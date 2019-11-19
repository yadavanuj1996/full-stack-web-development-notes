                                  Express.js

                                   PART I 
                                   (Intro)

                            Introduction to express

1) Express in an unopininated JS framework that sits upon NodeJS.Express is minimislitic 
   in design and does not have any rigid structure so developers can choose the architecture
   of express app.
2) Express is used to make things easy that can take a lot of complex code to achieve with
    plain NodeJS like to send a jpeg file using NodeJS in efficient manner takes around 45 lines
    using NodeJS while using express sendFile() function it takes one line.
3) Express has 4 main features: -
    i)   Middleware
    ii)  routing
    iii) subapplications
    iv)  conveniences

4) Middleware is poorly named, but it’s a term that’s not Express-specific and has been around  
   for a while. The idea is pretty simple: rather than one monolithic request handler function, 
   you call several request handler functions that each deal with a small chunk of the work. 
   These smaller request handler functions are called middleware functions, or middleware.

   One of the biggest features of middleware is that it’s relatively standardized, which means that lots of people have developed middleware for Express (including folks on the Express team). That means that if you can dream up the middleware, someone has probably already made it. There’s middleware to compile static assets like LESS and SCSS; there’s middleware for security and user authentication; there’s middleware to parse cookies and sessions.

5) At the end of the day, Express is just a Node.js module like any other.


                            Chapter 2. The basics of Node.js

1)  This chapter covers:- 

    Installing Node.js and using its module system
    Using package.json to describe your project’s metadata
    Using npm to install packages with npm install
    Doing two things at once with Node
    Using Node’s built-in http module to build a simple web server

2)  Node has a number of built-in modules, ranging from filesystem access in a module called 
    fs to utility functions in a built-in module called util.

3)  You’ll use Node’s require function to use the url module. require is similar to keywords 
    like import or include in other languages. require takes the name of a package as a string 
    argument and returns a package. There’s nothing special about the object 
    that’s returned—it’s often an object, but it could be a function or a string or a number. 
    The next listing shows how  you might use the url module.

4)  url module (Node.js)
    var url = require("url");
    var parsedURL = url.parse("http://www.example.com/profile?name=barry");
    console.log(parsedURL.protocol); // "http:"
    console.log(parsedURL.host); // "www.example.com"
    console.log(parsedURL.query); // "name=barry"

5)  “package dot json” is a pretty simple JSON file that defines project metadata like
    the name of the project, its version, and its authors. It also defines the project’s
    dependencies.
    {
        "name": "my-fun-project",
        "author": "Evan Hahn",
        "private": true,
        "version": "0.2.0",
        "dependencies": {}
    }

    Let’s say that you want to write a simple Node application that greets Nicolas Cage
    with the Mustache module.
    From the root of this directory, run npm install mustache --save. (You must run
    this command from the root of this directory so that npm knows where to put things.)
    This command creates a folder in this directory called node_modules. Then it
    downloads the latest version of the Mustache package and puts it into this new
    node_modules folder (look inside to check it out). The --save flag adds it to your
    package.json. Your package.json file should look similar to the one in the next listing,
    but it will now have the latest version of the Mustache package.
    {
        "name": "my-fun-project",
        "author": "Evan Hahn",
        "private": true,
        "version": "0.2.0",
        "dependencies": {
        "mustache": "^2.0.0"
    }

6)  npm init
    
    npm does much more than just install dependencies. For example, it allows you to
    autogenerate your package.json file. You can create package.json by hand, but 
    npm can do it for you.
    In your new project directory, you can type npm init. It will ask you a bunch of questions about your project—project name, author, version—and when it’s finished, it
    will save a new package.json. There’s nothing sacred about this generated file; you
    can change it all you want. But npm can save you a bit of time when creating these
    package.json files.    

7) exporting your own module
    var MAX = 100;
    function randomInteger() {
    return Math.floor((Math.random() * MAX));
    }
    module.exports = randomInteger;   

    REMEMBER module.exports can be anything you want. Anything to which
    you can assign a variable can be assigned to module.exports. It’s a function
    in this example, but it’s often an object. It could even be a string or a number
    or an array if you’d like.  

8) The two most common external resources you’ll deal with in Express are
    -Anything involving the filesystem—Like reading and writing files from your hard
     drive
    -Anything involving a network—Like receiving requests, sending responses, or
     sending your own requests over the internet

9)  First class functions are functions that are treated like an object (or are 
    assignable to a variable). Higher order functions are functions that take at 
    least one first class function as a parameter

10) http module is the reason we can make web servers using node.js.  
    ```
    var http = require("http");
    function requestHandler(request, response) {
    console.log("In comes a request to: " + request.url);
    response.end("Hello, world!");
    }
    var server = http.createServer(requestHandler);
    server.listen(3000); 
    ```
11) - Node’s module system makes use of a global function called require and a
      global object called module.exports. The two make for a straightforward module system.
    - You can use npm to install third-party packages from the npm registry.
    - Node.js has evented I/O. This means that when an event happens

                                Foundation of express

1)  This chapter covers  
    --  The four main features of Express:  
        – Middleware for letting a request flow  
          through multiple headers  
        – Routing for handling a request at a  
          specific spot  
        – Convenience methods and properties  
        – Views for dynamically rendering HTML  

2)  Although you can build full web servers with nothing but Node’s built-in http  
    module, you might not want to. As we discussed in chapter 1 and as you saw in  
    chapter 2, the API exposed by the http module is pretty minimal and doesn’t do a  
    lot of heavy lifting for you.  
    That’s where Express comes in: it’s a helpful third-party module (that is, not  
    bundled with Node). When you get right down to it, Express is an abstraction layer  
    This chapter covers  
    ■ The four main features of Express:  
    – Middleware for letting a request flow  
    through multiple headers  
    – Routing for handling a request at a  
    specific spot  
    – Convenience methods and properties  
    – Views for dynamically rendering HTML  

    on top of Node’s built-in HTTP server. You could, in theory, write everything with plain  
    vanilla Node and never touch Express. But as you’ll see, Express smooths out a lot of  
    the difficult parts and says “Don’t worry; you don’t need to deal with this ugly part.
    I’ll handle this!” In other words, it’s magic!  

3)  In a world without middleware, you’d find yourself having one master request function
    that handles everything. If you were to draw the flow of your application,
    Every request goes through just one request handler function, which eventually generates the response. That’s not to say that the master handler function can’t call other
    functions, but at the end of the day, the master function responds to every request.
    With middleware, rather than having your request pass through one function you
    write, it passes through an array of functions you write called a middleware stack.

4) logging middlewares, authorization middleware

5)  Third-party middleware libraries
    
    Like many parts of programming, it’s often the case that someone else has done what
    you’re trying to do. You can write your own middleware, but it’s common to find that
    the functionality you want is already available in somebody else’s middleware. Let’s
    look at a couple of examples of helpful third-party middleware.

    Morgan logging middleware
    ```
    git code  (3rd party github code)
    ```

6) EXPRESS’S STATIC MIDDLEWARE
    There’s more middleware out there than Morgan. It’s common for web applications
    to need to send static files over the wire. These include things like images or CSS or
    HTML—content that isn’t dynamic.
    express.static ships with Express and helps you serve static files. The simple act of
    sending files turns out to be a lot of work, because there are a lot of edge cases and
    performance considerations to think about. Express to the rescue!
    Let’s say you want to serve files out of a directory called public. The next listing
    shows how you might do that with Express’s static middleware.

    ```
    git code
    ```

    Why use path.resolve? (in code)

    What’s all that business about path.resolve? Why can’t you just say /public? The
    short answer is that you could, but it’s not cross-platform.
    On Mac and Linux, you want this directory:
    /public
    But on Windows, you want this directory:
    \public
    Node’s built-in path module will make sure that things run smoothly on Windows,
    Mac, and Linux

7) FINDING MORE MIDDLEWARE

    I’ve shown Morgan and Express’s static middleware, but there are more. Here are a
    few other helpful ones:-

    i)   connect-ratelimit — Lets you throttle connections to a certain number of requests
         per hour. If someone is sending numerous requests to your server, you can start
         giving them errors to stop them from bringing your site down.
    ii)  Helmet — Helps you add HTTP headers to make your app safer against certain
         kinds of attacks. We’ll explore it in later chapters. (I’m a contributor to Helmet,
         so I definitely recommend it!)
    iii) cookie-parser — Parses browser cookies.
    iv)  response-time — Sends the X-Response-Time header so you can debug the performance of        your application.

    If you’re looking for more middleware, you’ll have luck searching for “Express
    middleware,” but you should also search for “Connect middleware.”

8) Routing
    Routing is a way to map requests to specific handlers depending on their URL and
    HTTP verb. You could imagine having a homepage and an about page and a 404 page    

    ```
    git code routing
    ```
    
    These routes can get smarter. In addition to matching fixed routes, they can match
    more complex ones (imagine a regular expression or more complicated parsing), as
    shown in the next listing.
    app.get("/hello/:who", function(request, response) {
        response.end("Hello, " + request.params.who + ".");
    });

9)   Extending request and response

    Express augments the request and response objects that you’re passed in every
    request handler. The old stuff from Node.js is still there, but Express adds some new stuff too! The
    API docs (http://expressjs.com/api.html) explain everything, but let’s look at a couple of examples.
    
    One nicety Express offers is the redirect method. The following listing shows how
    it might work.
    ```
    response.redirect("/hello/world");
    response.redirect("http://expressjs.com");
    ```
    If you were just using Node, response would have no method called redirect;
    Express adds it to the response object for you. You can do this in vanilla Node, but it’s
    a lot more code.
    
    Express adds methods like sendFile, which lets you send a whole file, as the following listing shows.
    `response.sendFile("/path/to/cool_song.mp3");

10) Once again, the sendFile method isn’t available in vanilla Node; Express adds it for
    you. And just like the redirect example shown previously, you can do this in vanilla
    Node, but it’s a lot more code.
    It’s not only the response object that gets conveniences—the request object gets a
    number of other cool properties and methods, like request.ip to get the IP address
    or the request.get method to get incoming HTTP headers.
    Let’s use some of these things to build middleware that blocks an evil IP address.
    Express makes this pretty easy, as shown here.
        ```
        var express = require("express");
        var app = express();
        var EVIL_IP = "123.45.67.89";
        app.use(function(request, response, next) {
            if (request.ip === EVIL_IP) {
                response.status(401).send("Not allowed!");
            } 
            else {
                next();
            }
        });
        // ... the rest of your app ... 
        ```

        Notice that you’re using req.ip, a function called res.status(), and res.send().
        None of these are built into vanilla Node—they’re all extensions added by Express.
        Conceptually, there’s not much to know here, other than the fact that Express extends
        the request and response

11) Summary
    i)   Express sits on top of Node’s HTTP functionality. It abstracts away a lot of its
         rough edges.
    ii)  Express has a middleware feature that allows you to pipeline a single request
         through a series of decomposed functions.
    iii) Express’s routing feature lets you map certain HTTP requests to certain functionality.      For example, when visiting the homepage, certain code should be run.
    iv)  Express’s view-rendering features let you dynamically render HTML pages.
    v)   Many templating engines have been ported to work with Express. A popular
         one is called EJS, which is the simplest for folks who know already HTML. 


                                PART II (CORE)

                                  Middleware

1) This chapter covers
    i)   Writing middleware functions: a function with three arguments.
    ii)  Writing and using error-handling middleware: a function with four arguments
    iii) Using open source middleware functions, like Morgan for logging and 
         express.static for serving static files

2) Why use npm start?
    Why use npm start at all—why don’t you run node app.js instead? There are three
    reasons you might do this.
    It’s a convention. Most Node web servers can be started with npm start, regardless
    of the project’s structure. If instead of app.js someone had chosen application.js,
    you’d have to know about that change. The Node community seems to have settled
    on a common convention here.
    It allows you to run a more complex command (or set of commands) with a relatively
    simple one. Your app is pretty simple now, but starting it could be more complex in
    the future. Perhaps you’ll need to start up a database server or clear a giant log file.
    Keeping this complexity under the blanket of a simple command helps keep things
    consistent and more pleasant.
    The third reason is a little more nuanced. npm lets you install packages globally, so
    you can run them just like any other terminal command. Bower is a common one, letting you install front-end dependencies from the command line with the bower command. You install things like Bower globally on your system. npm scripts allow you to
    add new commands to your project without installing them globally, so that you can
    keep all of your dependencies inside your project, allowing you to have unique versions per project. This comes in handy for things like testing and build scripts, as
    you’ll see down the line.
    At the end of the day, you could run node app.js and never type npm start, but I
    find the reasons just mentioned compelling enough to do it.

    Sick of restarting your server?
    So far, when you change your code, you have to stop your server and start it again.
    This can get repetitive! To alleviate this problem, you can install a tool called nodemon, which will watch all of your files for changes and restart if it detects any.
    You can install nodemon by running npm install nodemon --global.
    Once it’s installed, you can start a file in watch mode by replacing node with nodemon
    in your command. If you typed node app.js earlier, just change it to nodemon app.js,
    and your app will continuously reload when it changes.

3)  Adding static file middleware to the middleware stack   
    ```
    app.use(function(req, res, next) {
        // …
    });
    ```
    ```
    app.use(function(req, res, next) {
        var filePath = path.join(__dirname, "static", req.url);
        fs.stat(filePath, function(err, fileInfo) {
            if (err) {
                next();
                return;
            }
            if (fileInfo.isFile()) {
                res.sendFile(filePath);
            } 
            else {
                next();
            }
        });
    });
    ```
    Sick of restarting your server?
    So far, when you change your code, you have to stop your server and start it again.
    This can get repetitive! To alleviate this problem, you can install a tool called nodemon, which will watch all of your files for changes and restart if it detects any.
    You can install nodemon by running npm install nodemon --global.
    Once it’s installed, you can start a file in watch mode by replacing node with nodemon
    in your command. If you typed node app.js earlier, just change it to nodemon app.js,
    and your app will continuously reload when it changes.

4)  Your final middleware: the 404 handler    
        ```
        app.use(function(req, res) {
            res.status(404);
            res.send("File not found!");
        });
        ```
        morgan logger function
        ```
        var express = require("express");
        var morgan = require("morgan");
        var app = express();
        app.use(morgan("short")); 

        or 

        var morganMiddleware = morgan("short");
        app.use(morganMiddleware);
        ```

        static path middleware
        ```
        var express = require("express");
        var morgan = require("morgan");
        var path = require("path");
        var app = express();
        app.use(morgan("short"));
        var staticPath = path.join(__dirname, "static");
        app.use(express.static(staticPath));
        app.use(function(req, res) {
        res.status(404);
        res.send("File not found!");
        });
        app.listen(3000, function() {
        console.log("App started on port 3000");
        });
        ```

5) Error handling middleware
    Remember when I said that calling next would continue on to the next middleware? I
    lied. It was mostly true but I didn’t want to confuse you.
    There are two types of middleware. You’ve been dealing with the first type so far—
    regular middleware functions that take three arguments (sometimes two when next is
    discarded). Most of the time, your app is in normal mode, which looks only at these
    middleware functions and skips the other.
    There’s a second kind that’s much less-used: error-handling middleware. When
    your app is in error mode, all regular middleware is ignored and Express will execute
    only error-handling middleware functions. To enter error mode, simply call next with
    an argument. It’s convention to call it with an error object, as in next(new Error
    ("Something bad happened!")).
    These middleware functions take four arguments instead of two or three. The first
    one is the error (the argument passed into next), and the remainder are the three
    from before: req, res, and next. You can do anything you want in this middleware.
    When you’re done, it’s just like other middleware: you can call res.end or next. Calling next with no arguments will exit error mode and move onto the next normal middleware; calling it with an argument will continue onto the next error-handling
    middleware if one exists.
    Let’s say you have four middleware functions in a row. The first two are normal,
    the third handles errors, and the fourth is normal.

    If no errors happen, it’ll be as if the error-handling middleware never existed. To reiterate more precisely, “no errors” means “next was never called with any arguments.” If
    an error does happen, then Express will skip over all other middleware until the first
    error-handling middleware in the stack. It might look like figure 4.8.
    While not enforced, error-handling middleware is conventionally placed at the end of
    your middleware stack, after all the normal middleware has been added. This is beca

    Express’s error-handling middleware does not handle errors that are thrown with the
    throw keyword, only when you call next with an argument.
    Express has some protections in place for these exceptions. The app will return a
    500 error and that request will fail, but the app will keep on running. Some errors like
    syntax errors, however, will crash your server

    ```
    res.sendFile(filePath, function(err) {
    if (err) {
        console.error("File failed to send.");
    } 
    else {
        console.log("File sent!");
    }
    });
    ```
    Instead of printing the success story to the console, you can enter error mode by calling
    next with an argument if there’s an error. You can do something like this next listing.
    
    ```
    app.use(function(req, res, next) {
        res.sendFile(filePath, function(err) {
            if (err) {
                next(new Error("Error sending file!"));
            }
        });
    });

    ```

6)  app.use(function(err, req, res, next) {
        console.error(err);
        next(err);
    });
    // …
    Now, when an error comes through, you’ll log it to the console so that you can investigate
    it later. But there’s more that needs to be done to handle this error. This is similar to
    before—the logger did something, but it didn’t respond to the request. Let’s write that part.
    You can add this code after the previous middleware. This will simply respond to
    the error with a 500 status code.
    // …
    app.use(function(err, req, res, next) {
        res.status(500);
        res.send("Internal server error.");
    });    

7) Other useful 3rd party middle wares
    http://expressjs.com/en/resources/middleware.html  // all middlewares

8) Summary
    ■ Express applications have a middleware stack. When a request enters your
    application, requests go through this middleware stack from the top to the bottom, unless they’re interrupted by a response or an error.
    ■ Middleware is written with request handler functions. These functions take two
    arguments at a minimum: first, an object representing the incoming request;
    second, an object representing the outgoing response. They often take a function that tells them how to continue on to the next middleware in the stack.
    ■ There are numerous third-party middleware written for your use. Many of these
    are maintained by Express developers.

                                    Routing

1) This chapter covers
    ■ Simple and pattern-matching routing
    ■ Using middleware with routing
    ■ Serving static files with express.static, Express’s built-in static file middleware
    ■  Using Express with Node’s built-in HTTPS module.

2)     
    Routers in action: the main app

    var express = require("express");
    var path = require("path");
    var apiRouter = require("./routes/api_router");
    var app = express();
    var staticPath = path.resolve(__dirname, "static");
    app.use(express.static(staticPath));
    app.use("/api", apiRouter);
    app.listen(3000);

    A sample router definition (at routes/api_router.js)    
    ```
    var express = require("express");
    var ALLOWED_IPS = [
        "127.0.0.1",
        "123.456.7.89"
    ];
    var api = express.Router();
    api.use(function(req, res, next) {
        var userIsAllowed = ALLOWED_IPS.indexOf(req.ip) !== -1;
        if (!userIsAllowed) {
            res.status(401).send("Not authorized!");
        } 
        else {
            next();
        }
    });
    api.get("/users", function(req, res) { /* ... */ });
    api.post("/user", function(req, res) { /* ... */ });
    
    api.get("/messages", function(req, res) { /* ... */ });
    api.post("/message", function(req, res) { /* ... */ });
    module.exports = api;
    ```

3)  
    Earlier we saw how cumbersome and long it was to do the same with plain
    Node.js using fs module reading file checking the fileInfo and then 
    returning it.

    app.get("/users/:userid/profile_photo", function(req, res) {
        res.sendFile(getProfilePhotoPath(req.params.userid));
    });

    path.resolve and path.join works because the windows treat path diffetent than
    mac and linux /abc vs \abc
    
4)  Using HTTPS with an Express app

    var express = require("express");
    var https = require("https");
    var fs = require("fs");
    var app = express();
    // ... define your app ...
    var httpsOptions = {
    key: fs.readFileSync("path/to/private/key.pem"),
    cert: fs.readFileSync("path/to/certificate.pem")
    };
    https.createServer(httpsOptions, app).listen(3000);     

5)  Summary
    ■ Routing is a mapping of an HTTP verb (like GET or POST) and a URI (like
    /users/123).
    ■ Routing can map to a simple string. It can also match against patterns or regular expressions.
    ■ Express has the ability to parse query strings.
    ■ As a convenience, Express has a built-in middleware for serving static files.
    ■ Routers can be used to split your application into many smaller applications,
    which is useful for code organization.
    ■ You can use Express with HTTPS by starting the server with your certificates


                                    Building APIs

1) This chapter covers
    ■ Using Express to build an API
    ■ HTTP methods and how they respond to
    common CRUD operations
    ■ Versioning your API using Express’s routers
    ■ Understanding HTTP status codes 

2) A simple Express-powered JSON API
    Now that you know what an API is, let’s build a simple one with Express. The 
    fundamentals of an Express API are pretty straightforward: take a request, parse it, and
    respond with a JSON object and an HTTP status code. You’ll use middleware and routing
    to take requests and parse them, and you’ll use Express’s conveniences to respond
    to requests.

    NOTE Technically, APIs don’t have to use JSON—they can use other data
    interchange formats like XML or plain text. JSON has the best Express integration, 
    plays nicely with browser-based JavaScript, and is one of the most popular API choices,
    so we’ll use it here. You can use other formats if you want to.

3)  Random no API

    var express = require("express");
    var app = express();
    app.get("/random/:min/:max", function(req, res) {
    var min = parseInt(req.params.min);
    var max = parseInt(req.params.max);
    if (isNaN(min) || isNaN(max)) {
        res.status(400);
        res.json({ error: "Bad request." });
        return;
    }
    var result = Math.round((Math.random() * (max - min)) + min);
        res.json({ result: result });
    });
    app.listen(3000, function() {
        console.log("App started on port 3000");
    });

4) For handling versions of api in express we use following approach
    ```
    var express = require("express");
    var apiVersion1 = require("./api1.js");
    var apiVersion2 = require("./api2.js");
    var app = express();
    app.use("/v1", apiVersion1);
    app.use("/v2", apiVersion2);
    app.listen(3000, function() {
        console.log("App started on port 3000");
    });
    ```
    Note the api called using /v1 and /v2 will run the express routers and response
    differently as both are fetched from seperate files.

5)  Each range has a certain theme. Steve Losh sent a great tweet that summarizes
    them (which I had to paraphrase a bit), as told from the perspective of the server:
    HTTP status ranges in a nutshell:
    1xx: hold on
    2xx: here you go
    3xx: go away
    4xx: you messed up
    5xx: I messed up

     Remember the first principle of good API design;
    defining your own HTTP status codes wouldn’t be what people expect. People expect
    you to stick to the usual suspects.

    WHAT ABOUT HTTP 2? Most HTTP requests are HTTP 1.1 requests, with a
    handful of them still using version 1.0. HTTP 2, the next version of the standard, is slowly being implemented and rolled out across the web. Luckily,
    most of the changes happen at a low level and you don’t have to deal with
    them. HTTP 2 does define one new status code—421—but that shouldn’t
    affect you much

6) Sending HTTP codes
    In Express, the default status code is 200. If a user visits a URL where no resource is
    found and your server doesn’t have a request handler for it, Express will send a 404
    error. If you have some other error in your server, Express will send a 500 error

    so send manually use
      `  res.status(404); inside any request handler before sending the response object.

       ` res.status(404).json({ error: "Resource not found!" });

       `res.statusCode = 404; Node.js way above are express way

7)  The 100 range
    
    There are only two official status codes in the 100 range: 
    
    100 (Continue) and 
    101 (Switching Protocols). 
    
    You’ll likely never deal with these yourself. If you do, check the
    specification or the list on Wikipedia.
    Look at that! You are already one-fifth of the way through the status codes.
    
    The 200 range
    
    Steve Losh summarized the 200 range as “here you go.” The HTTP spec defines several
    status codes in the 200 range, but four of them are by far the most common.
    
    200: OK

    200 is the most common HTTP status code on the web by a long shot. HTTP calls status
    code 200 OK, and that’s pretty much what it means: everything about this request and
    response went through just fine. Generally, if you’re sending the whole response just
    fine and there aren’t any errors or redirects (which you’ll see in the 300s section),
    then you’ll send a 200 code.
   
    201: CREATED

    Code 201 is very similar to 200, but it’s for a slightly different use case. It’s common for
    a request to create a resource (usually with a POST or a PUT request). This might be
    creating a blog post, sending a message, or uploading a photo. If the creation succeeds and everything’s fine, you’ll want to send a 201 code. This is a bit nuanced, but
    it’s typically the correct status code for the situation.
    
    202: ACCEPTED

    Just as 201 is a variant of 200, 202 is a variant of 201.
    I hope I’ve beaten it into your head by now: asynchronousity is a big part of Node
    and Express. Sometimes you’ll asynchronously queue a resource for creation but it
    won’t be created yet.
    If you’re pretty sure that the request wants to create a valid resource (perhaps
    you’ve checked that the data is valid) but you haven’t created it yet, you can send a 202
    status code. It effectively tells the client, Hey, you’re all good, but I haven’t made the
    resource yet.
    Sometimes you’ll want to send 201 codes and other times you’ll want to send 202;
    it depends on the situation.
    
    204: NO CONTENT

    204 is the delete version of 201. When you create a resource, you typically send a 201
    or a 202 message. When you delete something, you often don’t have anything to
    respond with other than Yeah, this was deleted. That’s when you typically send a 204
    code. There are a few other times when you don’t need to send any kind of response
    back, but deletion is the most common use case.
    
    The 300 range
    There are several status codes in the 300 range, but you’ll really only set three of
    them, and they all involve redirects.

    301: MOVED PERMANENTLY

    HTTP status code 301 means Don’t visit this URL anymore; see another URL. 301
    responses are accompanied with an HTTP header called Location, so you know where
    to go next.
    You’ve probably been browsing the web and have been redirected—this probably
    happened because of a 301 code. This usually occurs because the page has moved.

    303: SEE OTHER

    HTTP status code 303 is also a redirect, but it’s a bit different. Just like code 200 is for
    regular requests and 201 is for requests where a resource is created, 301 is for regular
    requests and 303 is for requests where a resource is created and you want to redirect
    to a new page.

    307: TEMPORARY REDIRECT

    There’s one last redirect status code: 307. Like the 301 code, you’ve probably been
    browsing the web and been redirected because of a 307 code. They’re similar, but they
    have an important distinction. 301 signals Don’t visit this URL ever again; see another
    URL; 307 signals See another URL just for now. This might be used for temporary maintenance on a URL.
    
    The 400 range
    
    The 400 range is the largest, and it generally means that something about the request
    was bad. In other words, the client made a mistake and it’s not the server’s fault.
    There are a lot of different errors here.

    401 AND 403: UNAUTHORIZED AND FORBIDDEN ERRORS

    There are two different errors for failed client authentication: 401 (Unauthorized)
    and 403 (Forbidden). The words unauthorized and forbidden sound pretty similar—
    what’s the difference?
    In short, a 401 error occurs when the user isn’t logged in. A 403 error occurs when
    the user is logged in as a valid user, but they don’t have permissions to do what they’re
    trying to do.
    Imagine a website where you couldn’t see any of it unless you logged in. This website also has an administrator panel, but not all users can administer the site. Until you
    logged in, you’ll see 401 errors. Once you logged in, you’ll stop seeing 401 errors. If
    you tried to visit the administrator panel as a non-admin user, you’d see 403 errors.
    Send these response codes when the user isn’t authorized to do whatever they’re
    doing.
    
    404: NOT FOUND
    
    I don’t think I have to tell you much about 404—you’ve probably run into it when
    browsing the web. One thing I found a little surprising about 404 errors is that you
    can visit a valid route but still get a 404 error.
    For example, let’s say you want to visit a user’s page. The homepage for User #123
    is at /users/123. But if you mistype and visit /users/1234 and no user exists with ID
    1234, you’ll get a 404 error.
    OTHER ERRORS
    There are a lot of other client errors you can run into—far too many to enumerate
    here. Visit the list of status codes at https://en.wikipedia.org/wiki/List_of_HTTP_
    status_codes to find the right status code for you.
    When in doubt about which client error code to use, send a 400 Bad Request error.
    It’s a generic response to any kind of bad request. Typically, it means that the request
    has malformed input—a missing parameter, for example. Although there might be a
    status code that better describes the client error, 400 will do the trick.
    
    The 500 range
    
    The final range in the HTTP specification is the 500 range, and although there are several errors in this range, the most important one is 500: Internal Server Error. Unlike
    400 errors, which are the client’s fault, 500 errors are the server’s fault. They can be for
    any number of reasons, from an exception to a broken connection to a database error.
    Ideally, you should never be able to cause a 500 error from the client—that would
    mean that your client could cause bugs in your server.
    If you catch an error and it really does seem to be your fault, then you can respond
    with a 500 error. Unlike the rest of the status codes where you want to be as descriptive
    as possible, it’s often better to be vague and say “Internal Server Error”; that way hackers can’t know where the weaknesses in your system lie. We’ll talk much more about
    this in chapter 10 when we talk about security.

8) Summary
    ■ An API in the context of Express is a web service that accepts requests and
    returns structured data (JSON in many cases).
    ■ The fundamentals of building an API with Express involve using its JSON and
    routing features heavily.
    ■ HTTP methods and how they relate to common application actions. GET typically corresponds to reading, POST typically corresponds to creation, PUT
    typically corresponds to changing, and DELETE typically responds to removal.
    ■ Versioning your API is helpful for compatibility. Express’s router feature helps
    you create different versions of your API.
    ■ There are lots of HTTP status codes (code 404 is perhaps the most famous). A
    good API uses these status codes properly       

                                Views

1) Rendering non-HTML views
    Express’s default content type is HTML, so if you don’t do anything special, res.render will render your responses and send them to the client as HTML. Most of the
    time, I find this to be enough. But it doesn’t have to be this way. You can render plain
    text, XML, JSON, or whatever you want. Just change the content-type by changing the
    parameter to res.type:
    app.get("/", function(req, res) {
        res.type("text");
        res.render("myview", {
            currentUser: "Gilligan"
        });
    });
    There are often better ways to render some of these things—res.json, for example,
    should be used instead of a view that renders JSON—but this is another way to do it.

2) Summary
    ■ Express has a view system that can dynamically render HTML pages. You call
    res.render to dynamically render a view with some variables. Before doing this,
    you must configure Express to use the right view engine in the right folder.
    ■ The EJS templating language is a light layer on top of HTML that adds the ability
    to dynamically generate HTML with pieces of JavaScript.
    ■ The Pug templating language is a reimagining of HTML that lets you dynamically render HTML with a whole new language. It attempts to remove verbosity
    and typing.


                                PART III
                            EXPRESS IN CONTEXT


                     Persisting your data with MongoDB


1)  Code:- 
    https://repl.it/@SuperCoder1/learn-about-me

    This chapter covers
    ■ Using Mongoose, an official MongoDB library
    for controlling the database with Node
    ■ Securely creating user accounts using bcrypt
    ■ Using Passport for user authentication.

2) 2 types of db classification
    i) Relational (SQL) ex:- MySql, PostgresSQL    
    ii) Non-relational (No-SQL) ex:- MongoDB

    Typically, relational databases are a lot like spreadsheets. Their data is structured,
    and each entry is generally a row in a table. They’re a bit like strongly typed languages
    such as Java, where each entry must fit into rigid requirements (called a schema).
    Most relational databases can be controlled with some derivative of SQL, the Structured Query Language; you likely have heard of MySQL or SQL Server or PostgreSQL.
    The terms relational databases and SQL databases are often used interchangeably.
    Non-relational databases are often called NoSQL databases. (NoSQL means anything
    that isn’t SQL, but it tends to refer to a certain class of database.) I like to imagine
    NoSQL as a different technology and a fist-up cry against the status quo. Perhaps
    NoSQL is tattooed on a protester’s arm. In any case, NoSQL databases are different
    from relational databases in that they’re generally not structured like a spreadsheet.
    They’re generally a bit less rigid than SQL databases. They’re very much like JavaScript in this way; JavaScript is generally less rigid. In general, NoSQL databases feel a
    bit more like JavaScript than SQL databases

3) Mongoose is to Mongo as Sequelize is to SQL.

4) How Mongo works
    Before we start, let’s talk about how Mongo works. Most applications have one database, like Mongo. These databases are hosted by servers. A Mongo server can have
    many databases on it, but there is generally one database per application. If you’re
    developing only one application on your computer, you’ll likely have only one Mongo
    database. (These databases can be replicated across multiple servers, but you treat
    them as if they’re one database.)
    To access these databases, you’ll run a Mongo server. Clients will talk to these servers,
    viewing and manipulating the database. There are client libraries for most programming 
    languages; these libraries are called drivers and let you talk to the database
    in your favorite programming language. In this book, we’ll be using the Node driver
    for Mongo.
    
    Every database will have one or more collections. I like to think of collections as
    fancy arrays. A blog application might have a collection for blog posts, or a social network might have a collection for user profiles. They’re like arrays in that they’re giant
    lists, but you can also query them (“Give me all users in this collection older than age
    18,” for example) much more easily than arrays.
    Every collection will have any number of documents. Documents aren’t technically
    stored as JSON, but you can think of them that way; they’re basically objects with 
    various properties. Documents are things like users and blog posts; there’s one document
    per thing. Documents don’t have to have the same properties, even if they’re in the
    same collection—you could theoretically have a collection filled with completely different 
    objects (although you seldom do this in practice).
    Documents look a lot like JSON, but they’re technically Binary JSON, or BSON. You
    almost never deal with BSON directly; rather, you’ll translate to and from JavaScript
    objects. The specifics of BSON encoding and decoding are a little different from JSON.
    BSON also supports a few types that JSON does not, like dates, timestamps, and undefined values

5) For you SQL users out there
    If you come from a relational/SQL background, many of Mongo’s structures map oneto-one with structures from the SQL world. (If you’re not familiar with SQL, you can
    skip this section.)
    Documents in Mongo correspond with rows or records in SQL. In an application
    with users, each user would correspond to one document in Mongo or one row in
    SQL. In contrast to SQL, Mongo doesn’t enforce any schema at the database layer, so
    it’s not invalid in Mongo to have a user without a last name or an email address that’s
    a number.

    Imp terms:- 
        Document 
        Collection
        Database
        Application
    

    Collections in Mongo correspond to SQL’s tables. Mongo’s collections contain
    many documents, whereas SQL’s tables contain many rows. Once again, Mongo’s collections don’t enforce a schema, unlike SQL. In addition, these documents can embed
    other documents, unlike in SQL—blog posts could contain the comments, which
    would likely be two tables in SQL. In a blog application, there would be one Mongo
    collection for blog posts or one SQL table. Each Mongo collection contains many documents, where each SQL table contains many rows or records.
    Databases in Mongo are very similar to databases in SQL. Generally, there’s one
    database per application. Mongo databases can contain many collections, whereas
    SQL databases can contain many tables. A social networking site would likely have just
    one of these databases in SQL, Mongo, or another type of database.
    For a full list of translations from SQL terminology to Mongo terminology (queries,
    too), check out the official SQL to MongoDB Mapping Chart at http://docs.mongodb
    .org/manual/reference/sql-comparison/index.html.

6) Mongoose, MongoDB and Node
    You’ll need a library that will let you talk to Mongo from Node, and therefore from
    Express. There are a number of lower-level modules, but you’d like something easy to
    use and feature filled. What should you use?
    Look no further than Mongoose (http://mongoosejs.com/), an officially supported
    library for talking to Mongo from Node. To quote its documentation:
    Mongoose provides a straight-forward, schema-based solution to modeling
    your application data and includes built-in type casting, validation, query
    building, business logic hooks and more, out of the box.
    In other words, Mongoose gives you much more than merely talking to the database.
    You’ll learn how it works by creating a simple website with user accounts.

7) THE BCRYPT-NODE MODULE This example (listing 8.1) uses a module called
    bcrypt-node. This module is written in pure JavaScript just like most other
    modules so it’s easy to install. There’s another module on the npm registry
    called bcrypt, which requires some C code to be compiled. Compiled C code
    will be faster than pure JavaScript, but it can cause issues if your computer
    isn’t set up correctly for compiling C code. We use bcrypt-node in this example to avoid those issues here.
    When it’s time to get more speed, you should switch to the bcrypt module.
    Luckily, the faster module is almost identical once it’s installed, so it should
    be quick to swap it out.

8)  Comments on project code
    Note that we use bcrypt.compare instead of a simple equality check
    (with something like ===). This is for security reasons—it helps keep us safe from a complicated hacker trick called a timing attack.

    Setting body-parser’s extended option to false makes the parsing simpler and more
    secure. The next listing shows how to add sign-up routes in routes.js. 

9)  body-parser—parses HTML forms
    ■ cookie-parser—handles the parsing of cookies from browsers and is required
    for user sessions
    ■ express-session—Stores user sessions across different browsers
    ■ connect-flash—Shows error messages
    ■ passport.initialize—Initializes the Passport module (as you’ll learn)
    ■ passport.session—Handles Passport sessions (as you’ll learn)

10) app.use(session({
    secret: "TKRv0IJs=HYqrvagQ#&!F!%V]Ww/4KiVs$s,<<MX",

    resave: true,
        saveUninitialized: true
    }));
    app.use(flash());
    app.use(passport.initialize());
    app.use(passport.session());

    There are three options we pass to express-session:
    ■ secret allows each session to be encrypted from the clients. This deters hackers
    from hacking into users’ cookies. As noted, it needs to be a bunch of random
    characters.
    ■ resave is option required by the middleware. When it’s set to true, the session will
    be updated even when it hasn’t been modified.
    ■ saveUninitialized is another required option. This resets sessions that are
    uninitialized.

11)  Summary
    ■ Mongo is a database that lets you store arbitrary documents.
    ■ Mongoose is an official Mongo library for Node. It works well with Express.
    ■ To securely create user accounts, you need to make sure you never store passwords directly. You’ll use the bcrypt module to help us do this.
    ■ You’ll use Passport to authenticate users, making sure they’re logged in before
    they can perform certain operations.    


                              Testing Express applications

1) 


                                 Best Practices

1) This chapter covers
    ■ Benefits of simplicity in your code
    ■ Structuring your app’s files
    ■ Using the npm shrinkwrap command to lock down dependency versions for reliability
      (and the benefits of doing so)
    ■ Avoiding installing modules globally

2) file structure (check attached 'express structure.png' image)

    package.json should come as no surprise—it’s present in every Node project. This will have
    all of the app’s dependencies as well as all of your npm scripts. You’ve seen different incarnations of this file throughout the book and it’s not different in a big app.
    ■ app.js is the main application code—the entry point. This is where you call express()
    to instantiate a new Express application. It is also where you put middleware
    that’s common to all routes, like security or static file middleware. This file
    doesn’t start the app, as you’ll see—it assigns the app to module.exports.
    ■ bin is a folder that holds executable scripts relevant to your application. There’s often
    just one (listed here), but sometimes more are required.
    – bin/www is an executable Node script that requires your app (from
    app.js) and starts it. Calling npm start should run this script.
    ■ config is a folder that’ll hold any configuration for your app. It’s often full of JSON files
    that specify things like default port numbers or localization strings.
    ■ public is a folder that’s served by static file middleware. It’ll have any static files
    inside—HTML pages, text files, images, videos, and so on. The static file middleware will also serve any of public’s subfolders. The HTML5 Boilerplate at
    Figure 12.1 A common folder
    structure for Express applications
    Licensed to <miler.888@gmail.com> www.it-ebooks.info
    Locking down dependency versions 221
    https://html5boilerplate.com/, for example, presents a good selection of common static files you might add here.
    ■ routes is a folder that holds numerous JavaScript files, each one exporting an Express
    router. You might have a router for all URLs that start with /users and another
    for all that start with /photos. Chapter 5 has all the details about routers and
    routing—check out section 5.3 for examples of how this works.
    ■ test is a folder that holds all of your test code. Chapter 9 has all the juicy details
    about this.
    ■ views is a folder that holds all of your views. Typically they’re written in EJS or Pug,
    as shown in chapter 7, but there are many other templating languages you
    can use. 

3) The best way to see an app that has most of these conventions is by using the official
    Express application generator. You can install this with 
    `npm install -g expressgenerator
    Once it’s installed, you can run express my-new-app and it’ll create a
    folder called my-express-app with a skeleton app set up, as shown in figure 

4)  Node has far and away the best dependency system . A coworker said, in
    describing Node and npm: “They nailed it.”
    npm uses semantic versioning (sometimes shortened to semver) for all of its packages. 
    Versions are broken up into three numbers: major, minor, and patch. For example, version 
    1.2.3 is major version 1, minor version 2, and patch version 3.
    In the rules of semantic versioning, a major version upgrade can have a change
    that is considered breaking. A breaking change is one where old code wouldn’t be
    compatible with new code. For example, code that worked in Express major version
    3 doesn’t necessarily work with major version 4. Minor version changes are, by
    contrast, not breaking. They generally mean a new feature that doesn’t break existing
    code. Patch versions are for, well, patches—they’re reserved for bug fixes and
    performance enhancements. Patches shouldn’t break your code; they should generally
    make things better.

    MAJOR VERSION ZERO There’s one asterisk to this: basically anything goes if
    the major version is 0. The whole package is considered to be unstable at
    that point.

5)  Short way to locking down dependency  versions.
    Example of optimistic versioning
        ```
        // …
        "dependencies": {
        "express": "^5.0.0",
        "ejs": "~2.3.2"
        }
    // …
        ```


    The ^ character indicates optimistic versioning is allowed. You’ll get all patch and minor
    updates. The ~ character indicates a slightly less optimistic versioning. You’ll get only
    patch updates.
    If you’re editing your package.json, you can specify the dependency to an exact
    version. The previous example would look like this next listing.

    Example of omitting optimistic versioning
        ```
        // …
        "dependencies": {
        "express": "5.0.0",
        "ejs": "2.3.2"
        }
        // …
        ```
    Removing the ^ and ~ characters from the version number indicates only that specific
    version of the package should be downloaded and used. These edits are relatively easy
    to do and can lock a package down to a specific version.
    If you’re installing new packages, you can turn off npm’s optimistic versioning by
    changing the --save flag to –save-exact. For example, npm install --save express
    becomes npm install --save-exact express. This will install the latest version of
    Express, just like always, but it won’t mark it optimistically in your package.json—it’ll
    specify an exact version.

6) Long, thourough and most foolproof way to locking down dependency  versions.
     npm’s shrinkwrap command

    The problem with the short and previous solution is that it doesn’t lock down 
    subdependency versions. npm has a subcommand called shrinkwrap that solves this problem.
    Let’s say you’ve run npm install and everything works just fine. You’re at a state
    where you want to lock down your dependencies. At this point, run a single command
    from somewhere in your project:
        ```
        npm shrinkwrap
        ```
    You can run this in any Node project that has a package.json file and dependencies. If
    all goes well, there will be a single line of output: wrote npm-shrinkwrap.json. (If it
    fails, it’s likely because you’re executing this from a non-project directory or are
    missing a package.json file.)

    The next time you issue npm install, it won’t look at the packages in package.json 
    —it’ll look at the files in npm-shrinkwrap.json and install from there. Every
    time npm install runs, it looks for the shrinkwrap file and tries to install from there.
    If you don’t have one (as we haven’t for the rest of this book), it’ll look at 
    package.json. As with package.json, you typically check npm-shrinkwrap.json into 
    version control. This allows all developers on the project to keep the same package 
    versions, which is the whole point of shrink-wrapping!

7)  Upgrading and adding dependencies
    
    This is all good once you’ve locked in your dependencies, but you probably don’t
    want to freeze all of your dependencies forever. You might want to get bug fixes or
    patches or new features—you just want it to happen on your terms.
    To update or add a dependency, you’ll need to run npm install with a package
    name and a package version. For example, if you’re updating Express from 4.12.0 to
    4.12.1, you’ll run npm install express@4.12.1. If you want to install a new package
    (Helmet, for example), run npm install helmet. This will update the version or
    add the package in your node_modules folder, and you can start testing. Once it all
    looks good to you, you can run npm shrinkwrap again to lock in that dependency
    version.
    Sometimes, shrink-wrapping isn’t for you. You might want to get all of the latest
    and greatest features and patches without having to update manually. Sometimes,
    though, you want the security of having the same dependencies across all installations
    of your project. 

8)  Download all dependencies locally including the likes of grunt and mocha( used for
    testing).

    The other way to do this is by adding the command as an npm script. Once again, let’s
    say that you want to run Mocha. The next listing shows how you’d specify that as an
    npm script.
    ``
    // …
    "scripts": {
    "test": "mocha"
    },
    // …
    ``