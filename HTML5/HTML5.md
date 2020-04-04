							HTML 5 (Front End)

1) `<!Doctype html>`
	is written so that the browser know the doctument has to be rendered according to the full standard mode decided by W3C for HTML ,CSS
	there are three modes:- quirks, almost standard and full standard as in starting the standard was for netscape browser and msft 	browser internet explorer.
2)	Nowdays most of the browsers use full standard mode
3)	The <head></head> section contains elements that will not be displayed on web browser it will contain elements like <title>, <meta> 		tags link for favicon and author name.

	<title> will define title for the page that will be displayed on tab of browser and on bookmarks.
	<meta charset="utf-8"> will let our web page containg all sort of characters available including all makor languages of the world.
	<meta name="author" content="Chris Mills">    AUTHOR NAME
	<meta name="description" content="The MDN Web Docs Learning Area aims to provide complete beginners to the Web with all they need to 			know to get started with developing web sites and applications."> for defining description that will also play role in SEO.

	<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">    for displaying favicon
	<link rel="stylesheet" href="css/style.css">
	<script src="jsfolder/comp.js">
	<html lang="en-US"> for defining the standard language for our web page.
4) 	Block Elements vs Inline Elements
	Block Element	
	a) Block elements are the ones which contain all the space of parent element(container) they usually break the line and start from new 		   line.
	b) Block level may contain other block element, data or any inline element.
	c) By default, block-level elements begin on new lines, but inline elements can start anywhere in a line.
	ex:- <div>,<p>,<ul>,<ol>,<lo>,<table>,<section>
	
	Inline elements
	a) Inline elements does not create new line and can be created inside another block level element, they can start from anywhere and 		   does not need to start from new line.
	b) Inline level may contain other inlilne level element and data but cannot contain block level elements.
	c) By default, inline elements do not force a new line to begin in the document flow
	ex:- <b>,<strong>,<a>,<img>,<input>
5) 	<div> is a block element,<span> is inline.
	This means that to use them semantically, divs should be used to wrap sections of a document, while spans should be used to wrap small 		portions of text, images, etc.
6) 	Forms
	HTML Forms are one of the main points of interaction between a user and a web site or application. They allow users to send data to 		the web site. Most of the time that data is sent to the web server, but the web page can also intercept it to use it on its 		own.	
	<form action="/my-handling-form-page" method="post">
	  <div>
	    <label for="name">Name:</label>
	    <input type="text" id="name" name="user_name">
	  </div>
	  <div>
	    <label for="mail">E-mail:</label>
	    <input type="email" id="mail" name="user_mail">
	  </div>
	  <div>
	    <label for="msg">Message:</label>
	    <textarea id="msg" name="user_message"></textarea>
	  </div>
	</form>
7) 	Form Validation
	Client-side validation is validation that occurs in the browser before the data has been submitted to the server. Client-side 		validation is more user-friendly than server-side validation because it gives an instant response. 
	a) Client-side validation is further subdivided into the following categories:
		-JavaScript validation is coded using JavaScript. This validation is completely customizable.
		-Built-in form validation uses HTML5 form validation features. 
	b) Server-side validation is validation that occurs on the server after the data has been submitted.
	required keyword is used in html 5 to make it required , minlength will determine minimum length that has to be entered maxlength is 		maximum length that has to be entered while min and max are for numbers.
	type="password" type="number" type="text" type="email" are all valid for putting in input element

		<form>
		  <div>
		    <label for="choose">Would you prefer a banana or a cherry?</label>
		    <input type="text" id="choose" name="i_like" required minlength="6" maxlength="6">
		  </div>
		  <div>
		    <label for="number">How many would you like?</label>
		    <input type="number" id="number" name="amount" value="1" min="1" max="10">
		  </div>
		  <div>
		    <button>Submit</button>
		  </div>
		</form>
8)	Some important tags for html forms
	<input> it is a self closing tag
	<textarea></textarea>
	<label></label>
	
	<input type="radio" name="gender" value="male" checked> Male<br>
  	<input type="radio" name="gender" value="female"> Female<br>  
  	
	<input type="password" minlength="8">
	
	<input type="checkbox" name="vehicle1" value="Bike"> I have a bike<br>
 	<input type="checkbox" name="vehicle2" value="Car"> I have a car<br>

9) 	The web is based on a very basic client/server architecture that can be summarized as follows: a client (usually a Web browser) sends 		a request to a server (most of the time a web server like Apache, Nginx, IIS, Tomcat, etc.), using the HTTP protocol. The server 	 answers the request using the same protocol.


	On the client side, an HTML form is nothing more than a convenient user-friendly way to configure an HTTP request to send data to a 		server. This enables the user to provide information to be delivered in the HTTP request.
	
	<form action="http://foo.com" method="get">
	action will contain the target api url or script where the data will go and method will contain the type of HTTP request most common 		ones that we will be using are (get) and (post).

	required and 
10)     For Get request the data goes in the parameter GET  (abc.com?say=Hi&to=mom)
	
	Get request looks like 
	/?say=Hi&to=Mom HTTP/2.0
	Host: foo.com
	
	Post request looks like
	POST / HTTP/2.0
	Host: foo.com
	Content-Type: application/x-www-form-urlencoded
	Content-Length: 13

	say=Hi&to=Mom

	Get is used when updates or insertion are made while POST is used when we have to pass data and expect something from server. Post 		sends the data in body so it is more secure so we should use post if data is critical.

11) 	The enctype attributeSection.This attribute lets you specify the value of the Content-Type HTTP header included in the request 		generated when the form is submitted. This header is very important because it tells the server what kind of data is being sent. By 		default, its value is application/x-www-form-urlencoded. In human terms, this means: "This is form data that has been encoded into URL 		parameters."

If you want to send files, you need to take three extra steps:

1) Set the method attribute to POST because file content can't be put inside URL parameters.
2) Set the value of enctype to multipart/form-data because the data will be split into multiple parts, one for each file plus one for the text data included in the form body (if text is also entered into the form).
3) Include one or more File picker widgets to allow your users to select the file(s) that will be uploaded.
For example:

<form method="post" enctype="multipart/form-data">
  <div>
    <label for="file">Choose a file</label>
    <input type="file" id="file" name="myFile">
  </div>
  <div>
    <button>Send the file</button>
  </div>
</form>
 
12) Meta tags
	<meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScrit" > for SEO 
	<meta name="viewport" content="width=device-width, initial-scale=1.0">	


