---
layout: post
title: "Java Updates."
date: 2014-07-01
---

Since I've been working on my Java server I've noticed some additions to Java that I hadn't previously been using! I started programming in Java around 2008, so new things have actually been introduced to Java since my initial experiences with the language. 

Initially I figured I'd need to use InputStreamWriter, a while loop, and build the character codes into a String to translate my files into HTML. Not that case anymore! Since Java 7, there are a few new utility classes for dealing with files and paths. The ones I've utilized so far are [Files][fs], [Paths][p], and [File][f].

For example:

{% highlight Java %}
//Old version (more or less)
public String fileToString(path) throws Exception {
		InputStream inputStream = new FileInputStream(path);
		Reader reader = new InputStreamReader(inputStream, "UTF-8");

		int data;
		do {
				data = reader.read();
		    char theChar = (char) data;
		} while(data != -1)
		reader.close();
		return reader.toString();
}

//Using Files and Paths
public String fileToString(path) throws Exception {
    byte[] encoded = Files.readAllBytes(Paths.get(path));
    return new String(encoded, StandardCharsets.UTF_8);
}
{% endhighlight %}

Thats a lot more concise and convenient! 

In addition I've found that Java functions (including constructors) can now take optional parameters. The notation is `String... vargs`. Unfortunately this is not as useful as I'd hoped. Rather than using this new feature I decided to keep using method overloading. Introducing optional parameters requires testing whether or not that variable was passed into the method. Method overloading feels more clear to me, although that may simply be out of habit and my familiarity with dealing with optional parameters in Java. 

[f]: http://docs.oracle.com/javase/8/docs/api/java/io/File.html
[fs]: http://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html
[p]: http://docs.oracle.com/javase/8/docs/api/java/nio/file/Paths.html