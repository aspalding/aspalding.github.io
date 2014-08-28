---
layout: post
title: "Maven, JRuby scripting containers, and JRuby load paths."
date: 2014-08-28
---

While integrating a JRuby project in a Java project managed by Maven I ran into some difficulty getting everything integrated together nicely. This was essential as I wanted my program to be reproducible by others. While this may not be the optimal solution, I struggled to find another solution to my issue and couldn't find a more optimal solution in [JRuby's github wiki pages][jrgh]. 

Using Bundler was problematic because Maven uses its own version of JRuby that does not share the same gem path as a system wide installation. 

The relevant modifications to your `pom.xml` file are as follows: 

{% highlight xml %}
<repositories>
    <repository>
        <id>rubygems-releases</id>
        <url>http://rubygems-proxy.torquebox.org/releases</url>
    </repository>
</repositories>
...
<dependency>
    <groupId>org.jruby</groupId>
    <artifactId>jruby-complete</artifactId>
    <version>1.7.13</version>
</dependency>

<dependency>
	<groupId>rubygems</groupId>
    <artifactId>rttt</artifactId>
    <version>0.1</version>
    <type>gem</type>
</dependency>
...
<plugin>
	<groupId>de.saumya.mojo</groupId>
	<artifactId>gem-maven-plugin</artifactId>
	<version>1.0.5</version>
	<configuration>
	    <jrubyVersion>1.7.13</jrubyVersion>
	    <includeRubygemsInResources>true</includeRubygemsInResources>
	</configuration>
	<executions>
	    <execution>
	        <goals>
	            <goal>initialize</goal>
	        </goals>
	    </execution>
	</execution>
</plugin>
{% endhighlight %}

This defines where to download the gems from, the JRuby should be included, that a specific gem should be included, and finally a gem-maven-plugin that lets Maven pull the dependancies. With this setup, all your gems are pulled into `target/rubygems/gems`.

Finally you need to add the path of the gem to your load path. 

{% highlight Java %}
private final static String jrubyhome = "/src/ruby/lib/";
private final static String filename = jrubyhome + "web.rb";
private final static String gemhome = System.getProperty("user.dir") + "/target/rubygems/gems/rttt-0.1/lib";

ScriptingContainer container = new ScriptingContainer();
List<String> loadPaths = new ArrayList<String>();
loadPaths.add(jrubyhome);
loadPaths.add(gemhome);
container.setLoadPaths(loadPaths);

Object object = container.runScriptlet(PathType.RELATIVE, filename);
{% endhighlight %}

Here we simply define where are Ruby files are located and they are added to the load path of the ScriptingContainer. Now we can finally use our gem! Unfortunately this solution is not optimal. For example, if my project had many gem dependancies it would be incredibly tedious to load each path the same way as above. Unfortunately I could not find a better solution due to my unusual use case of JRuby. Most of the resources available seem to utilize JRuby as a solution to enhance Ruby's multithreaded performance. Rails on JRuby specifically seems to be the most important goal of the JRuby team. 

That being said! I had a set of requirements, and this solution at least makes it possible to move forward. 

[jrgh]: https://github.com/jruby/jruby/wiki/Jruby-Scripting-container-using-Gems-with-a-Maven-Project