Download Link: https://assignmentchef.com/product/solved-64831-assignment-1-http-web-proxy-server
<br>
Adapted<strong> from Kurose &amp; Ross – Computer Networking: a top-down approach featuring the Internet</strong>

<strong>CBOK categories: Abstraction, Design, Data &amp; Information, Networking, Programming</strong>

In this practical, you will learn how web proxy servers work and one of their basic functionalities caching.

<h1>Task</h1>

Your task is to develop a small web proxy server which is able to cache web pages.

It is a very simple proxy server which only understands simple HTTP/1.1 GET-requests but is able to handle all kinds of objects – not just HTML pages, but also images.

<h1>Very Important</h1>

<em>Although this practical is marked automatically, all marks will be moderated by a marker using the following information.</em>

You must add a comment explaining the changes you’ve made to <strong><em>each</em></strong> of your svn repository commits. In other words, each commit should explain what was changed in the code and why briefly (e.g. it may be a bug fix or a protocol behaviour fix).

We should be able to review your development process and see the changes made to code with each version you have committed. <strong>Please keep in mind that we can check the number of lines of code as well as actual code changes made with each commit.</strong>

During manual marking and plagiarisms checks, we will look look at your development process. If we do not see a clear path to a solution (i.e. code changes and regular commits and comments reflecting your learning to develop the protocol you <strong>will forfeit 50% of the marks allocated for this programming assignment and in the extreme case you will be allocated a mark of  0%. An</strong>

<strong>example case of a 0% would be the sudden appearance of working code passing multiple tests</strong>.

It is up to you to provide evidence of your development process.




<h2>Introduction</h2>

In this practical, you will learn how web proxy servers work and one of their basic functionalities, <strong>caching</strong>. Generally, when a client (e.g. your browser) makes a web request the following occurs:

<ol>

 <li>The client sends a request to the web server</li>

 <li>The web server then processes the request</li>

 <li>The web server sends back a response message to the requesting client And let’s say that the entire transaction takes 500 ms.</li>

</ol>

In order to improve the performance, we create a proxy server between the client and the web server. The proxy server will act as a middle-man for the web transactions. Requesting a web request will now occur in the following steps:

<ol>

 <li>The client sends a request to the proxy server</li>

 <li>Skip to step 7 If the proxy server has cached the response</li>

 <li>Forward the request to the web server</li>

 <li>The web server processes the request</li>

 <li>The web server sends a response back to the proxy server</li>

 <li>The proxy server caches the response</li>

 <li>The proxy server returns the cached response to the client</li>

</ol>

On the first request, the transaction may be a fraction longer than the previous example. However, subsequent requests will be significantly faster due to reduced network latency and server load (sometimes less than 10 ms).

The mechanism for caching can be as simple as storing a copy of a resource on the proxy servers file system.

The standard you are using, HTTP1.1, in your programming assignment is described in detail in

<a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D">RFCs (request for comments) [see:</a> <a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D"><strong>https://en.wikipedia.or</strong></a><a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D"><strong>g</strong></a><a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D"><strong>/wiki/Request_for_Comments</strong></a><a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D"><strong>]</strong></a>

<a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D"><strong>(https://en.wikipedia.or</strong></a><a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D"><strong>g</strong></a><a href="https://en.wikipedia.org/wiki/Request_for_Comments%5D"><strong>/wiki/Request_for_Comments%5D)</strong></a>

<a href="https://tools.ietf.org/html/rfc2616">HTTP1.1 RFC we use is 2616 [</a><a href="https://tools.ietf.org/html/rfc2616"><strong>https://tools.ietf.or</strong></a><a href="https://tools.ietf.org/html/rfc2616"><strong>g</strong></a><a href="https://tools.ietf.org/html/rfc2616"><strong>/html/rfc2616</strong></a>

<a href="https://tools.ietf.org/html/rfc2616"><strong>(https://tools.ietf.or</strong></a><a href="https://tools.ietf.org/html/rfc2616"><strong>g</strong></a><a href="https://tools.ietf.org/html/rfc2616"><strong>/html/rfc2616) </strong></a><a href="https://tools.ietf.org/html/rfc2616">] </a>

Please read <strong>Section 5.1.2</strong> in RFC 2616.

You can read more about caching and how it is handled in HTTP in RFC 2616 in <strong>Section 13</strong>.

<strong><em>Now we want you to aim for the correct protocol/proxy behavior (see the marking rubric at the end of the practical description for what we will look for).</em></strong>

<h2>Steps for approaching the practical</h2>

<h3>Step 1</h3>

Understand the HTTP/1.1 requests/responses of the proxy. Your proxy MUST be able to handle GET requests from a client. Your proxy may handle other request types (such as POST) but this is not required.

You need to know the following:

<ol>

 <li>What HTTP request will the browser send to the proxy?</li>

 <li>What will HTTP response look like?</li>

 <li>In what ways will the response look different if it comes from the proxy than if it comes from the origin server (i.e. the server where the original page is stored?). You will not be able to test this yet, but what do you think would happen?</li>

</ol>

<h3>Step 2</h3>

Understand the socket connections:

<ol>

 <li>How will the client know to talk to the proxy?</li>

 <li>What host and port number will the proxy be on?</li>

 <li>The proxy may need to connect to the origin server (if the web object is not in the cache), what host and port number will the proxy connect to?</li>

 <li>Where will the proxy get the web object information?</li>

</ol>

<h3>Step 3: Checkpoint</h3>

Make sure you have the answers to steps 1 &amp; 2 before you go any further.

You can’t code it if you don’t know what should happen.

Ask questions on the discussions forum if you are unsure above the above.

<h3>Step 4: Python Code</h3>

<a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1">Now that you know what should be happening, have a look at the code </a><a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1"><strong>here</strong></a> <a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1"><strong> </strong></a>

<a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1"><strong>(https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1) </strong></a><a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1">.</a>

Look at the interactions you identified in steps 1 &amp; 2 and see where they would occur in the code.

Review the python code presented in the sockets lecture. You’ll find details of the socket calls in the <a href="https://docs.python.org/2.7/library/socket.html">Python Socket library documentation </a><a href="https://docs.python.org/2.7/library/socket.html"><strong>https://docs.p</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>y</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>thon.or</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>g</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>/2.7/librar</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>y</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>/socket.html</strong></a>

<a href="https://docs.python.org/2.7/library/socket.html"><strong>(https://docs.p</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>y</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>thon.or</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>g</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>/2.7/librar</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>y</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>/socket.html)</strong></a>

<a href="https://docs.python.org/2.7/library/socket.html"><strong> (https://docs.p</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>y</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>thon.or</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>g</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>/2.7/librar</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>y</strong></a><a href="https://docs.python.org/2.7/library/socket.html"><strong>/socket.html) </strong></a><strong><em>You won’t just be able to copy the lecture code</em></strong>, but it shows you the key steps; creating sockets, connecting sockets, sending data on sockets and receiving data on sockets.

Your task is to make the correct socket calls and supply the correct arguments for those calls.

You will <strong>only</strong> need to fill in the code between the comment lines.

The comments above the comments lines give you hints to the code to insert.

<h3>Step 5: Differences in Python and C</h3>

If you are new to python, look at the code structure. Most of the code is given to you with your focus just on adding the networking code. A couple of things that are different in Python than in the C derived languages:

<ol>

 <li>Python uses whitespace to indicate code blocks and end of lines. Note there are no brackets or braces { } around code blocks and no semi-colons ; at the end of lines. The indentation isn’t just important for readability in Python, it affects how your code runs. Make sure you indent code blocks correctly.</li>

 <li>Python has a tuple data structure. So functions can return more than one value, or more precisely return one tuple with multiple values, but the syntax allows the parenthesis to be left off. Tuples appear in the lecture slides in the line:</li>

</ol>

The accept() call returns a tuple of two values, the first value is the new socket and the second is the address information. This is the same as:

<h3>Step 6</h3>

Start with getting the proxy working when a cached file is requested. Where it will return the response itself and does not have to contact the origin server

<h3>Step 7</h3>

Once that is working, add the code to handle the case where the file is not cached by the proxy and the proxy must request it from the origin server.

<h3>Step 8</h3>

In both steps 6 &amp; 7, make use of both <em>telnet</em> utility <em>and</em> a browser to test your proxy server. You can also use <strong>Wireshark</strong> to capture what is being sent/received from the origin server.

<h2>Running your proxy in the labs and Websub</h2>

The labs and test machines are running Python 2.7. Make sure that your submission is compatible with Python 2 and does not use Python 3 features that are not backward compatible with Python 2.7.

The University proxy will intercept any attempt to connect to a host outside of the University and require authentication (which is outside the scope of this practical), thus, your proxy will not be able to connect to origin servers outside of the University when running on computers inside the University. When testing inside the University, use URLs within the University infrastructure. This should not affect you when running your proxy outside the University.

<h2>Running the Proxy Server</h2>

<a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1">Download the </a><a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1"><strong>template file</strong></a><a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1"><strong>  </strong></a><a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1"><strong>(https://myuni.adelaide.edu.au/courses/64831/files/8387551/download? download_frd=1) </strong></a><a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1"> and save it as </a><a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1">Proxy.py</a> <a href="https://myuni.adelaide.edu.au/courses/64831/files/8387551/download?download_frd=1">.</a>

Run the following command in terminal to run the proxy server

your machine.

You can change 8888 as the port to listen to.

The skeleton code without any modifications should (tested on Python 2.7.5 on university systems) should go into an infinite loop. You can use Ctrl+C to terminate a program.

When you are ready to test your proxy server, open a Web browser and navigate to http://localhost:8888/http://autoidlab.cs.adelaide.edu.au

Note that when typing the proxy into the browser request in this way, the browser may only display the main page and may fail to download associated files such as images and style sheets. This is due to a difference in URI requirements when sending requests to a proxy vs sending to an origin Web server (we’ll look at this in the tutorials).

<h2>Configuring your Browser (Optional)</h2>

You can also directly configure your web browser to use your proxy if you want without using the URI.

This depends on your browser.

In Internet Explorer, you can set the proxy in <em>Tools &gt; Internet Options &gt; Connections tab &gt; LAN Settings</em>.

In Netscape (and derived browsers such as Mozilla), you can set the proxy in <em>Tools &gt; Options &gt; Advanced tab &gt; Network tab &gt; Connection Settings</em>.

In both cases, you need to give the address of the proxy and the port number that you set when you ran the proxy server. You should be able to run the proxy and the browser on the same computer without any problem. With this approach, to get a web page using the proxy server, you simply provide the URL of the page you want.

For example, running http://autoidlab.cs.adelaide.edu.au would be the same as running http://localhost:8888/http://autoidlab.cs.adelaide.edu.au

Set up like this, the browser should successfully load both the main web page and all associated files due to reasons we’ll discuss in tutorials.

<h2>Testing your code</h2>

When it comes time to test your code, cUrl and telnet are useful tool to use.

If you want to test on an image that is the same as the web submission system, you can ssh into:

uss.cs.adelaide.edu.au and then run and test your code.

Let’s have a look at these two tests:

<h3>Obtaining a remote web page</h3>

1 $ curl -si http://localhost:8080/http://autoidlab.cs.adelaide.edu.au/ | head -n 1 2 HTTP/1.1 200 OK

<a href="http://autoidlab.cs.adelaide.edu.au/">The above command requests </a><a href="http://autoidlab.cs.adelaide.edu.au/">http</a><a href="http://autoidlab.cs.adelaide.edu.au/"><span style="text-decoration: line-through;">:</span></a><a href="http://autoidlab.cs.adelaide.edu.au/">//autoidlab</a><a href="http://autoidlab.cs.adelaide.edu.au/">.</a><a href="http://autoidlab.cs.adelaide.edu.au/">cs</a><a href="http://autoidlab.cs.adelaide.edu.au/">.</a><a href="http://autoidlab.cs.adelaide.edu.au/">adelaide.edu</a><a href="http://autoidlab.cs.adelaide.edu.au/">.</a><a href="http://autoidlab.cs.adelaide.edu.au/">au</a>

<a href="http://autoidlab.cs.adelaide.edu.au/"><strong>(http://autoidlab.cs.adelaide.edu.au) </strong></a><a href="http://autoidlab.cs.adelaide.edu.au/"> via the Web proxy. </a><a href="http://autoidlab.cs.adelaide.edu.au/">-i</a><a href="http://autoidlab.cs.adelaide.edu.au/"> prints out re</a>sponse with headers and -s removes additional output and head -n 1 extracts the first line from the cUrl command.

The result is the first line in the response from the proxy. This response should match if you were talking directly to the origin server, like so

<h3>Handle page that does not exist</h3>

1 $ curl -sI http://localhost:8080/http://autoidlab.cs.adelaide.edu.au/fakefile.html | head -n 1 2 HTTP/1.1 404 Not Found

The response for a path that doesn’t exist shows the above status code. Your proxy to work correctly will also need to handle this case too.

<h3>Using <strong>telnet</strong></h3>

<strong>Note</strong> that we used the absolute URL because telnet here is connected to you proxy and not the origin server.

If you are very unfamiliar and having trouble, this video demo recorded by David showing an example use of both tools to connect and send GET requests will be handy. <strong><em>Note that in the video, David is not connecting to a proxy but connecting to a web server and issuing HTTP requests to the web server</em></strong>:

<a href="https://tinyurl.com/cmf79nyb"><strong>https://tin</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>y</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>url.com/cmf79n</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>y</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>b</strong></a><strong><u>    </u></strong><a href="https://tinyurl.com/cmf79nyb"><strong> (https://tin</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>y</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>url.com/cmf79n</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>y</strong></a><a href="https://tinyurl.com/cmf79nyb"><strong>b)</strong></a>

<h3>Be aware! Using arbitrary URLs to for testing</h3>

When testing, be aware that for certain URLs, although you issue http:// requests, for security reasons, they might get directed to https://. It has now become common practice for most websites to redirect http:// to https://. So, you may have seen 30x like responses. This redirects your browser to goto the HTTPS secure web server. So when you tried to do something <a href="http://localhost:8888/http:/ecms.adelaide.edu.au/">like</a> <a href="http://localhost:8888/http:/ecms.adelaide.edu.au/"><strong>http://localhost:8888/http://ecms.adelaide.edu.au/</strong></a>

<a href="http://localhost:8888/http:/ecms.adelaide.edu.au/"><strong>(http://localhost:8888/http://ecms.adelaide.edu.au/) </strong></a><a href="http://localhost:8888/http:/ecms.adelaide.edu.au/"> </a><a href="http://localhost:8888/http:/ecms.adelaide.edu.au/">the bro</a>wser will read the response and load the HTTPS URL <strong><u>https://ecms.adelaide.edu.au,</u></strong> <strong>(<u>https://ecms.adelaide.edu.au%2C/) </u></strong> thus navigating away from your proxy.

Here are two you can use where there are no redirects.

<a href="http://autoidlab.cs.adelaide.edu.au/"><strong>http://autoidlab.cs.adelaide.edu.au/</strong></a><strong><u>    </u></strong><a href="http://autoidlab.cs.adelaide.edu.au/"><strong> (http://autoidlab.cs.adelaide.edu.au/)</strong></a>

<a href="http://jsonplaceholder.typicode.com/todos/1"><strong>http://</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>j</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>sonplaceholder.t</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>y</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>picode.com/todos/1</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong> (http://</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>j</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>sonplaceholder.t</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>y</strong></a><a href="http://jsonplaceholder.typicode.com/todos/1"><strong>picode.com/todos/1)</strong></a>

Here is a link to an image you can use to test on a file other than an html file.

http://autoidlab.cs.adelaide.edu.au/sites/default/files/projectimages/PeerTrack.jpg