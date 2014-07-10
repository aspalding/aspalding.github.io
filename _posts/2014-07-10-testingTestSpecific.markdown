---
layout: post
title: "Test-specific Subclassing!"
date: 2014-07-10
---

One of my tasks for the next week or two has been to review one of the videos from Uncle Bob's Clean Coder series and create a series of questions on the topics talked about. Luckily enough, the video I was assigned provided some useful advice for testing my current project! 

Testing classes and functions that depend on certain files or directories was really tricky. Initially I attempted to create a new class as well as an interface to mock the objects and pretend that the imaginary files did exist. However, this became burdensome as I needed to test additional file functionality. Uncle Bob suggests using "Test-Specific Subclasses" to test this sort of tricky behavior. Using this testing pattern I was able to only override the functions one at a time as I needed them for specific tests. For example:

{% highlight Java %}
public byte[] responseBody() throws Exception {
    if(file.isFile())
        //do something
    else if(file.isDirectory())
        //do something else
    else
        //404
}
{% endhighlight %}

The File object, file, is passed through the constructor (this is known as dependency injection). To test each conditional, each case requires a slightly different subclass. My testing code is listed below:

{% highlight Java %}
@Test
public void testValidFilePathResponseString() throws Exception {
    File fake = new File(""){
        @Override
        public boolean isFile(){
            return true;
        }
    };
    Response resp = new Response(fake);
    assertEquals("HTTP/1.1 200 OK\nContent-Type: null\n\n", resp.responseHeader(200, ""));
}

@Test
public void testValidDirectoryPathResponseString() throws Exception {
    File fake = new File(""){
        @Override
        public boolean isFile(){
            return false;
        }
        @Override
        public boolean isDirectory(){
            return true;
        }
    };
    Response resp = new Response(fake);
    assertEquals("HTTP/1.1 200 OK\nContent-Type: text/html\n\n", resp.responseHeader(200, ""));
}

@Test
public void testInvalidPathResponseString() throws Exception {
    File fake = new File(""){
        @Override
        public boolean isFile(){
            return false;
        }
        @Override
        public boolean isDirectory(){
            return false;
        }
    };
    Response resp = new Response(fake);
    assertEquals("HTTP/1.1 404 Not Found\n\n", resp.responseHeader(200, ""));
}
{% endhighlight %}

In my opinion this solution provides additional clarity to my tests opposed to my initial method of testing this function/class, it is obvious which conditional is being tested because the boolean the conditional depends on is established just above where the function is called! In addition it is less complex to write the test as you do not have to shift your focus back and forth between your separate mock class.  