---
layout: post
title: "On to the Java server."
date: 2014-06-26
---

The next project in my apprenticeship program is the Java server. Interestingly enough, quite a few of my fellow apprentices are and have been working on this project in the recent past. So I should be able to have some solid discussion if I get stuck! Today I attempted to get started but took a step back and decided to do some more research. 

In the past, I tended to get my runtime loop early so I can start manually testing my program as soon as possible. For this project (and my last two tic tac toe's) I've been practicing TDD as closely as possible. For TTT I knew what I needed to complete the program so the tests were not so difficult to come up with! My Java server could probably use a bit more planning beforehand since its a bit more complicated of a project. 

Anyway, heres a list of resources I've been exploring. 

* Clean Code and Principles Patterns and Practices
  * For planning my program with SOLID practices.
* [W3 Hypertext Transfer Protocol][w3]
  * Thorough documentation of the HTTP/1.1 specification.  
* [HTTP Status Code Reference][status]
  * Quick reference for HTTP status codes.
	* Should be helpful. I know a handful, but there are dozens! 
* [HTTP Made Really Easy][httpeasy]
	* Another reference of the HTTP spec. 
	* Reads a bit more easily that the formal W3 spec. 
* [What Is a Socket?][wias]
	* Documentation by Oracle/Sun (grr) about sockets.
	* Provides some Java specific information about sockets.
* Various Java Classes
	* java.net: [Socket][sock] and [SocketServer][sockserve].
	* java.lang: [Thread][thread] and [String Buffer][sb].
	* java.io: [InputStreamReader][isr], [OutputStreamWriter][osw], and [FileReader][fr].
	* java.util: [String Tokenizer][st].
	
I may or may not use all these classes but it'll be nice to know what to look for when I do need them. I'm hoping this project provides deeper knowledge of how the web works. Now I have to figure out how I should put the pieces together and what patterns I'll be using for the different pieces of the server! 



[w3]: http://www.w3.org/Protocols/rfc2616/rfc2616.html
[status]: http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml
[httpeasy]: http://www.jmarshall.com/easy/http/
[wias]: http://docs.oracle.com/javase/tutorial/networking/sockets/definition.html
[sock]: http://docs.oracle.com/javase/8/docs/api/java/net/Socket.html
[sockserve]: http://docs.oracle.com/javase/8/docs/api/java/net/ServerSocket.html
[thread]: http://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html
[isr]: http://docs.oracle.com/javase/8/docs/api/java/io/InputStreamReader.html
[osw]: http://docs.oracle.com/javase/8/docs/api/java/io/OutputStreamWriter.html
[fr]: http://docs.oracle.com/javase/8/docs/api/java/io/FileReader.html
[st]: http://docs.oracle.com/javase/8/docs/api/java/util/StringTokenizer.html
[sb]: http://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html
