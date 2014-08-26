---
layout: post
title: "Implementing custom routes on SimpleServer."
date: 2014-08-26
---

These past two days I've been working towards making my JavaServer reusable. To do this I've narrowed down the amount of routes to simply include a route that deals with files and directories. [SimpleServer](https://github.com/aspalding/SimpleServer) can take an additional argument that allows another developer to provide their own router. Two interfaces are defined that guide the behavior of custom routes and routers. 

As a foreword, this project depends on Maven and Java 1.8. This tutorial will implement the quintessential "Hello World!" application. 

To get started you should clone the repo and build the jar:

	git clone https://github.com/aspalding/SimpleServer.git
	cd SimpleServer && mvn package

Copy the jar into a new project directory:

	cp jars/SimpleServer.jar ../SimpleServerImpl/assets
	
Next the jar has to be imported into your project. If you are using IntelliJ navigate to file -> project structure -> Libraries -> + -> Java and select the jar file. If you are using maven add the following to your pom.xml:

{% highlight xml %}
<dependency>
    <groupId>SimpleServer</groupId>
	<artifactId>SimpleServer</artifactId>
    <version>1.0</version>
    <scope>system</scope>
    <systemPath>${project.basedir}/assets/SimpleServer.jar</systemPath>
</dependency>
{% endhighlight %}

For this post our server will simply say "Hello World!" in the browser. Implement your router as follows: 

{% highlight Java %}
public class HelloRouter implements Router {
    public Response route(Request request){
        return new Response(200, "OK", new HashMap<String, String>(), "Hello world!");
    }
}
{% endhighlight %}

Make another class containing main and put your custom router: 

{% highlight Java %}
public class HelloApplication {
    public static void main(String args[]){
        try {
            new Application().setUp(args);
            Application.runLoop(new HelloRouter());
        } catch(Exception e){
            System.out.println("There was a problem!");
        }
    }
}
{% endhighlight %}

To quickly test the server simply type:

	curl localhost:5000
	
You should receive the message "Hello World!" You may also type that address in your browser to see the result! 

In addition to the router interface, the jar contains a route interface for more specific functionality. 

An example of this is as follows: 

{% highlight Java %}
/* Implements Router interface */
public class HelloRouter implements Router {
    public Response route(Request request) {
        if (!request.path.equals(System.getProperty("user.dir") + "/"))
            return new HelloRoute(request).respond();
        else
            return new Response(200, "OK", new HashMap<String, String>(), "Hello world!");
    }
}

/* Implements Route interface */
public class HelloRoute implements Route {
    String name;

    public HelloRoute(Request request){
        this.name = request.path.substring(System.getProperty("user.dir").length() + 1);
    }

    public Response respond(){
        return new Response(200, "OK", new HashMap<String, String>(), "Hello " + name + "!");
    }
}
{% endhighlight %}

In addition to responding "Hello World!" this new application can also respond to a specific user by adding their name to the url, type: 

	curl localhost:5000/Barney
	
And the server will reply "Hello Barney!" 

If SimpleServer is not provided a custom implementation of Router it will simply server folders and files through the FileDirectoryRoute and SimpleRouter. SimpleRouter may be useful as the `else` condition or `default` switch in a custom Router. The SimpleRouter will display files on the hosts filesystem and will respond with a 404 response if a request has no corresponding file, directory, or defined route. 