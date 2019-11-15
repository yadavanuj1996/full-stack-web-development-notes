                    Introduction to Node

This post is a getting started guide to Node.js, the server-side JavaScript
runtime environment. Node.js is built on top of the Google Chrome V8
JavaScript engine, and it's mainly used to create web servers - but it's not
limited to that.

-Node.js is a runtime environment for JavaScript that runs on the server.

-Node.js is open source, cross-platform,

-Node.js is built on top of the Google Chrome V8 JavaScript engine

Advantages of Node.js
1) Fast:- 
    One of the main selling points of Node.js is speed. JavaScript code running on Node.js
    (depending on the benchmark) can be twice as fast than compiled languages like C or Java,
    and orders of magnitude faster than interpreted languages like Python or Ruby, because 
    of its non-blocking paradigm.

2) Simple

3) Javascript :-
    The paradigms are all the same, and in Node.js the new ECMAScript standards can be used first, 
    as you don't have to wait for all your users to update their browsers 
    - you decide which ECMAScript version to use by changing the Node.js version.

4) V8 Engine

5) Asynchronous Platform :- 
    Node provides non-blocking I/O primitives, and generally, 
    libraries in Node.js are written using non-blocking paradigms, making a blocking behavior an exception rather than the normal.When Node.js needs to perform an I/O operation, 
    like reading from the network, access a database or the filesystem, instead of 
    blocking the thread Node.js will simply resume the operations when the response comes back, instead of wasting CPU cycles waiting.

6) A huge number of libraries
    npm with its simple structure helped the ecosystem of node.js proliferate and now the npm
    registry hosts almost 500.000 open source packages you can freely use.


7) Simple Node ex:-

    ```
        const http = require('http')
        const hostname = '127.0.0.1'
        const port = 3000
        const server = http.createServer((req, res) => {
        res.statusCode = 200
        res.setHeader('Content-Type', 'text/plain')
        res.end('Hello World\n')
        })
        server.listen(port, hostname, () => {
        console.log(`Server running at http://${hostname}:${port}/`)
        })
    ```

    -The createServer() method of http creates a new HTTP server and returns it
    
    -The server is set to listen on the specified port and hostname. When the server is
    ready, the callback function is called, in this case informing us that the 
    server is running. Whenever a new request is received, the request event is called, 
    providing two objects: a request (an http.IncomingMessage object) and a response 
    (an http.ServerResponse object).

8)  In practice, this means that for the time being you use require() in Node and import in the
    browser.

9) Compilation

    JavaScript is generally considered an interpreted language, but modern JavaScript engines no
    longer just interpret JavaScript, they compile it.JavScript is internally compiled by 
    V8 with just-in-time (JIT) compilation to speed up the execution

10) Terminating Node.js program:- 
    The process core module is provides a handy method that allows you to programmatically
    exit from a Node.js program: process.exit() .
    When Node.js runs this line, the process is immediately forced to terminate.
    This means that any callback that's pending, any network request still being sent, any
    filesystem access, or processes writing to stdout or stderr - all is going to be ungracefully
    terminated right away.

11) 
        ```
        const express = require('express')
        const app = express()
        app.get('/', (req, res) => {
        res.send('Hi!')
        })
        How to exit from a Node.js program
        23
        app.listen(3000, () => console.log('Server ready'))

        ```
        
        Note: process does not require a "require", it's automatically available.


        ```
            const express = require('express')
            const app = express()
            app.get('/', (req, res) => {
            res.send('Hi!')
            })
            const server = app.listen(3000, () => console.log('Server ready'))
            process.on('SIGTERM', () => {
            server.close(() => {
            console.log('Process terminated')
            })
            })
        ```

        What are signals? Signals are a POSIX intercommunication system: a notification
        sent to a process in order to notify it of an event that occurred.
        SIGKILL is the signals that tells a process to immediately terminate, and would
        ideally act like process.exit() .
        SIGTERM is the signals that tells a process to gracefully terminate. It is the
        signal that's sent from process managers like upstart or supervisord and many
        others. You can send this signal from inside the program, in another function:
        process.kill(process.pid, 'SIGTERM')

12) Change to production mode, env file by default contains development mode.
    process.env.NODE_ENV // "development"

13) import modules

    ```
        const car = {
            brand: 'Ford',
            model: 'Fiesta'
        }
            module.exports = car
            //..in the other file
            const car = require('./car')
    ```
    exports.car = {
    brand: 'Ford',
    model: 'Fiesta'
    }
    And in the other file, you'll use it by referencing a property of your import:
    const items = require('./items')
    items.car
    or
    const car = require('./items').car

    What's the difference between module.exports and exports ?
    The first exposes the object it points to. The latter exposes the properties of the object it points
    to.


                            NPM

1) Introduction to npm
    npm is the standard package manager for Node.js.
    npm
    45
    In January 2017 over 350000 packages were reported being listed in the npm registry, making
    it the biggest single language code repository on Earth, and you can be sure there is a
    package for (almost!) everything.
    It started as a way to download and manage dependencies of Node.js packages, but it has
    since become a tool used also in frontend JavaScript.
    There are many things that npm does.
    Yarn is an alternative to npm. Make sure you check it out as well

2) If a project has a packages.json file, by running
    npm install
    it will install everything the project needs, in the node_modules folder,
     creating it if it's not existing already.

    Installing a single package
    You can also install a specific package by running

    npm install <package-name>

    --save installs and adds the entry to the package.json file dependencies

    --save-dev installs and adds the entry to the package.json file devDependencies

    Updating is also made easy, by running
    npm update
  
    npm will check all packages for a newer version that satisfies your versioning constraints.
    You can specify a single package to update as well:
    npm update <package-name>

    npm follows the semantic versioning (semver) standard

3) The package.json file supports a format for specifying command line tasks that 
    can be run by using
    
    npm run <task-name>
    
    For example:
    {
        "scripts": {
            "start-dev": "node lib/server-development",
            "start": "node lib/server-production"
        },
    }
    
    It's very common to use this feature to run Webpack:
    {
        "scripts": {
            "watch": "webpack --watch --progress --colors --config webpack.conf.js",
            "dev": "webpack --progress --colors --config webpack.conf.js",
            "prod": "NODE_ENV=production webpack -p --config webpack.conf.js",
        },
    }

    So instead of typing those long commands, which are easy to forget or mistype, you can run
    $ npm run watch
    $ npm run dev
    $ npm run prod

4) 
    When you install a package using npm (or yarn), you can perform 2 types of installation:
    a) local install
    b) global install

    By default, when you type an npm install command, like:
    npm install lodash

    the package is installed in the current file tree, under the node_modules subfolder.
    As this happens, npm also adds the lodash entry in the dependencies property of the
    package.json file present in the current folder.

    A global installation is performed using the -g flag:
    
    npm install -g lodash
    When this happens, npm won't install the package under the local folder, but instead, it will
    use a global location

    npm install lodash
    
    This is going to install the package in the local node_modules folder.
    To use it in your code, you just need to import it into your program using require :
    const _ = require('lodash)

5) The package-lock.json file
    The package-lock.json file is automatically generated when installing node
    packages. Learn what it's about. In version 5, npm introduced the package-lock.json file.
    What's that? You probably know about the package.json file, which is much more common
    and has been around for much longer. The goal of the file is to keep track of the
    exact version of every package that is installed so that a product is 100% reproducible
    in the same way even if packages are updated by their maintainers.
    This solves a very specific problem that package.json left unsolved. In package.json you can
    set which versions you want to upgrade to (patch or minor), using the semver notation, for
    example:
    if you write ~0.13.0 , you want to only update patch releases: 0.13.1 is ok, but 0.14.0
    is not.
    if you write ^0.13.0 , you want to update patch and minor releases: 0.13.1 , 0.14.0 and
    so on.
    if you write 0.13.0 , that is the exact version that will be used, always
    You don't commit to Git your node_modules folder, which is generally huge, and when you try
    to replicate the project on another machine by using the npm install command, if you
    specified the ~ syntax and a patch release of a package has been released, that one is going
    to be installed. Same for ^ and minor releases.
    If you specify exact versions, like 0.13.0 in the example, you are not affected by this
    problem.
    It could be you, or another person trying to initialize the project on the other side of the world
    by running npm install .
    So your original project and the newly initialized project are actually different. Even if a patch
    or minor release should not introduce breaking changes, we all know bugs can (and so, they
    will) slide in.
    The package-lock.json sets your currently installed version of each package in stone, and
    npm will use those exact versions when running npm install .
    This concept is not new, and other programming languages package managers (like
    Composer in PHP) use a similar system for years.
    The package-lock.json file
    
    The package-lock.json file needs to be committed to your Git repository, so it can be fetched
    by other people, if the project is public or you have collaborators, or if you use Git as a source
    for deployments.
    The dependencies versions will be updated in the package-lock.json file when you run npm
    update .

6) Use `npm list` command to find version of each packages installed. 

7) How to uninstall an npm Node package, locally or globally
    To uninstall a package you have previously installed locally (using npm install <packagename> in the node_modules folder, run
    npm uninstall <package-name>
    from the project root folder (the folder that contains the node_modules folder).
    Using the -S flag, or --save , this operation will also remove the reference in the
    package.json file.
    If the package was a development dependency, listed in the devDependencies of the
    package.json file, you must use the -D / --save-dev flag to remove it from the file:
    npm uninstall -S <package-name>
    npm uninstall -D <package-name>
    If the package is installed globally, you need to add the -g / --global flag:
    npm uninstall -g <package-name>

8) When is a package a dependency, and when is it a dev dependency?
    When you install an npm package using npm install <package-name> , you are installing
    it as a dependency. The package is automatically listed in the package.json file, 
    under the dependencies list (as of npm 5: before you had to manually specify --save ).
    When you add the -D flag, or --save-dev , you are installing it as a development
    dependency, which adds it to the devDependencies list.
    Development dependencies are intended as development-only packages, that are unneeded
    in production. For example testing packages, webpack or Babel.
    When you go in production, if you type npm install and the folder contains a package.json
    file, they are installed, as npm assumes this is a development deploy.
    You need to set the --production flag ( npm install --production ) to avoid installing those
    development dependencies.    

9)  Event Loop
    ```
    const bar = () => console.log('bar')
    const baz = () => console.log('baz')
    const foo = () => {
    console.log('foo')
    setTimeout(bar, 0)
        baz()
    }
    foo();

    This code prints, maybe surprisingly:
    foo
    baz
    bar
    ```
    When this code runs, first foo() is called. Inside foo() we first call setTimeout, 
    passing bar as an argument, and we instruct it to run immediately as fast as it can,
    passing 0 as the timer. Then we call baz().

    Why is this happening?
    The Message Queue
    When setTimeout() is called, the Browser or Node.js start the timer. Once the timer
    expires, in this case immediately as we put 0 as the timeout, the callback function is 
    put in the Message Queue. The Message Queue is also where user-initiated events like 
    click or keyboard events, or fetch responses are queued before your code has the
    opportunity to react to them. Or also DOM events like onLoad .

    The loop gives priority to the call stack, and it first processes everything it 
    finds in the call stack, and once there's nothing in there, it goes to pick up things
    in the event queue. We don't have to wait for functions like setTimeout , fetch or 
    other things to do their own work, because they are provided by the browser, and they
    live on their own threads. For example, if you set the setTimeout timeout to 2 seconds,
    you don't have to wait 2 seconds - the wait happens elsewhere.

9) ES6 Job Queue
    ECMAScript 2015 introduced the concept of the Job Queue, which is used by Promises 
    (also introduced in ES6/ES2015). It's a way to execute the result of an async function as 
    soon as possible, rather than being put at the end of the call stack.
    Promises that resolve before the current function ends will be executed right after 
    the current function.

    I find nice the analogy of a rollercoaster ride at an amusement park: the message queue puts
    you back in queue with after all the other people in the queue, while the job queue is the
    fastpass ticket that lets you take another ride right after you finished the previous one.
    Example:
    const bar = () => console.log('bar')
    const baz = () => console.log('baz')
    const foo = () => {
        console.log('foo')
        setTimeout(bar, 0)
        new Promise((resolve, reject) =>
            resolve('should be right after baz, before bar')
        ).then(resolve => console.log(resolve))
        baz()
    }
    foo()

    This prints
    foo
    baz
    should be right after baz, before bar
    bar

    That's a big difference between Promises (and Async/await, which is built on promises) and
    plain old asynchronous functions through setTimeout() or other platform APIs.

10) nextTick
    The Node.js process.nextTick function interacts with the event loop in a
    special way
    As you try to understand the Node.js event loop, one important part of it is
    process.nextTick() .
    Every time the event loop takes a full trip, we call it a tick.
    When we pass a function to process.nextTick() , we instruct the engine to invoke
    this function
    at the end of the current operation, before the next event loop tick starts:
    process.nextTick(() => {
        //do something
    })
    The event loop is busy processing the current function code.
    When this operation ends, the JS engine runs all the functions passed to nextTick calls
    during that operation.
    It's the way we can tell the JS engine to process a function asynchronously (after the current
    function), but as soon as possible, not queue it.
    Calling setTimeout(() => {}, 0) will execute the function in the next tick, much later than
    when using nextTick() .
    Use nextTick() when you want to make sure that in the next event loop iteration that code is
    already executed.
    nextTick

    setImmediate
    The Node.js setImmediate function interacts with the event loop in a special
    way
    When you want to execute some piece of code asynchronously, but as soon as possible, one
    option is to use the setImmediate() function provided by Node.js:
    setImmediate(() => {
    //run something
    })
    Any function passed as the setImmediate() argument is a callback that's executed in the next
    iteration of the event loop.
    How is setImmediate() different from setTimeout(() => {}, 0) (passing a 0ms timeout), and
    from process.nextTick() ?
    A function passed to process.nextTick() is going to be executed on the current iteration
    of the event loop, after the current operation ends. This means it will always
    execute before setTimeout and setImmediate .
    A setTimeout() callback with a 0ms delay is very similar to setImmediate() . The execution
    order will depend on various factors, but they will be both run in the next iteration
    of the event loop.

    Node.js also provides setImmediate() , which is equivalent to using 
    setTimeout(() => {}, 0) ,mostly used to work with the Node.js Event Loop.

11) setTimeout & setInterval
    NOTE: both this function will be feeded in message queue after the mentioned time
    and will be called when the call stack gets empty and the message queue of event
    loop starts.

    const id = setTimeout(() => {
    // should run after 2 seconds
    }, 2000)
    // I changed my mind
    clearTimeout(id)


    const id = setInterval(() => {
    // runs every 2 seconds
    }, 2000)
    clearInterval(id)

    setTimeout(() => {
    console.log('after ')
    }, 0)
    console.log(' before ')

    will print before after .
    and if promise is there the promise will run before the setTimeout. 


                            Callbacks
                        
1) Callbacks
    JavaScript is synchronous by default, and is single threaded. This means
    that code cannot create new threads and run in parallel. Find out what
    asynchronous code means and how it looks like

    ``` 
      JavaScript is synchronous by default and is single threaded. This means that
      code cannot create new threads and run in parallel.
    ``` 

2) Asynchronicity in Programming Languages
    Computers are asynchronous by design.
    Asynchronous means that things can happen independently of the main program flow.
    Callbacks
    100
    In the current consumer computers, every program runs for a specific time slot, and then it
    stops its execution to let another program continue its execution. This thing runs in 
    a cycle so fast that's impossible to notice, and we think our computers run many programs
    simultaneously, but this is an illusion (except on multiprocessor machines).
    Programs internally use interrupts, a signal that's emitted to the processor to gain
    the attention of the system.

    I won't go into the internals of this, but just keep in mind that it's normal for
    programs to be asynchronous, and halt their execution until they need attention, and 
    the computer can execute other things in the meantime. When a program is waiting for 
    a response from the network, it cannot halt the processor until the request finishes.
    
    Normally, programming languages are synchronous, and some provide a way to manage
    asynchronicity, in the language or through libraries. C, Java, C#, PHP, Go, Ruby, Swift,
    Python, they are all synchronous by default. Some of them handle async by using threads,
    spawning a new process.

3)    JavaScript (synchronous or asynchronous)
    
    JavaScript is synchronous by default and is single threaded. This means that code cannot
    create new threads and run in parallel.
    Lines of code are executed in series, one after another, for example:
        const a = 1
        const b = 2
        const c = a * b
        console.log(c)
        doSomething()

    But JavaScript was born inside the browser, its main job, in the beginning, was to 
    respond to user actions, like onClick , onMouseOver , onChange , onSubmit and so on. 
    How could it do this with a synchronous programming model?

    The answer was in its environment. The browser provides a way to do it by providing a set of
    APIs that can handle this kind of functionality.
    More recently, 
    
    Node.js introduced a non-blocking I/O environment to extend this concept to file access, 
    network calls and so on.
    
4) Callbacks
    
    You can't know when a user is going to click a button, so what you do is, you define 
    an event handler for the click event. This event handler accepts a function, which will
    be called when the event is triggered:

    document.getElementById('button').addEventListener('click', () => {
        //item clicked
    })
    This is the so-called callback.
    A callback is a simple function that's passed as a value to another function, and
    will only be executed when the event happens. We can do this because JavaScript has 
    first-class functions, which can be assigned to variables and passed around to other 
    functions (called higher-order functions)
    It's common to wrap all your client code in a load event listener on the window 
    object, which runs the callback function only when the page is ready:
    
        window.addEventListener('load', () => {
            //window loaded
            //do what you want
        })

    Callbacks are used everywhere, not just in DOM events.
    One common example is by using timers:
        setTimeout(() => {
        // runs after 2 seconds
        }, 2000)
   

5) Handling errors in callbacks
   
    How do you handle errors with callbacks? One very common strategy is to use what Node.js
    adopted: the first parameter in any callback function is the error object: error-first 
    callbacks If there is no error, the object is null . If there is an error, it contains
    some description of the error and other information.
    
        fs.readFile('/file.json', (err, data) => {
        if (err !== null) {
        //handle error
        console.log(err)
        return
        }
        //no errors, process data
        console.log(data)
        })

6) The problem with callbacks (or Callback Hell)
    Callbacks are great for simple cases!
    However every callback adds a level of nesting, and when you have lots of callbacks,
    the code starts to be complicated very quickly:

        window.addEventListener('load', () => {
            document.getElementById('button').addEventListener('click', () => {
                setTimeout(() => {
                    items.forEach(item => {
                    //your code here
                    })
                }, 2000)
            })
        })

    This is just a simple 4-levels code, but I've seen much more levels of nesting and it's not fun.
    How do we solve this?
    Alternatives to callbacks
    Starting with ES6, JavaScript introduced several features that help us with asynchronous code
    that do not involve using callbacks:
    Promises (ES6)
    Async/Await (ES8)



                            Promises

1) Introduction to promises
    A promise is commonly defined as a proxy for a value that will eventually become
    available.

    Promises are one way to deal with asynchronous code, without writing too many callbacks in
    your code.

    Although being around since years, they have been standardized and introduced in ES2015,
    and now they have been superseded in ES2017 by async functions.
    Async functions use the promises API as their building block, so understanding them is
    fundamental even if in newer code you'll likely use async functions instead of promises.
    
    How promises work, in brief
    Once a promise has been called, it will start in pending state. This means that the caller
    function continues the execution, while it waits for the promise to do its own processing, 
    and give the caller function some feedback.
  
    At this point, the caller function waits for it to either return the promise in a
    resolved state, or in a rejected state, but as you know JavaScript is asynchronous, 
    so the function continues its execution while the promise does it work.
    
    Which JS API use promises?
    In addition to your own code and libraries code, promises are used by standard modern Web
    APIs such as:
        the Battery API
        the Fetch API
        Service Workers
    It's unlikely that in modern JavaScript you'll find yourself not using promises, so 
    let's start diving right into them.

2) Creating a promise
    The Promise API exposes a Promise constructor, which you initialize using new Promise() :
    ```
    let done = true
    const isItDoneYet = new Promise(
        (resolve, reject) => {
            if (done) {
                const workDone = 'Here is the thing I built'
                resolve(workDone)
            } else {
                const why = 'Still working on something else'
                reject(why)
            }
        }
    )
    ```
    As you can see the promise checks the done global constant, and if that's true, we return a
    resolved promise, otherwise a rejected promise.
    Using resolve and reject we can communicate back a value, in the above case we just
    return a string, but it could be an object as well.
    Consuming a promise
   
3) Consuming promises
        In the last section, we introduced how a promise is created.
        Now let's see how the promise can be consumed or used.
        
        ```
        const isItDoneYet = new Promise(
            //...
        )
        const checkIfItsDone = () => {
            isItDoneYet
            .then((ok) => {
                console.log(ok)
            })
            .catch((err) => {
                console.error(err)
            })
        }
        ```
    Running checkIfItsDone() will execute the isItDoneYet() promise and will wait for it to
    resolve, using the then callback, and if there is an error, it will handle it in the catch
    callback.

4) Chaining promises
    A promise can be returned to another promise, creating a chain of promises.
    A great example of chaining promises is given by the Fetch API, a layer on top of the
    XMLHttpRequest API, which we can use to get a resource and queue a chain of promises to
    execute when the resource is fetched.
    The Fetch API is a promise-based mechanism, and calling fetch() is equivalent to defining
    our own promise using new Promise() .
    Example of chaining promises
        ```
        const status = (response) => {
            if (response.status >= 200 && response.status < 300) {
                return Promise.resolve(response)
            }
            return Promise.reject(new Error(response.statusText))
        }
        const json = (response) => response.json()
        fetch('/todos.json')
        .then(status)
        .then(json)
        .then((data) => { console.log('Request succeeded with JSON response', data) })
        .catch((error) => { console.log('Request failed', error) })
       
        ```
    In this example, we call fetch() to get a list of TODO items from the todos.json 
    file found in the domain root, and we create a chain of promises.
    Running fetch() returns a response, which has many properties, and within those we
    reference:
    status , a numeric value representing the HTTP status code
    statusText , a status message, which is OK if the request succeeded
    response also has a json() method, which returns a promise that will resolve with the
    content of the body processed and transformed into JSON.

    So given those premises, this is what happens: the first promise in the chain is a 
    function that we defined, called status() , that checks the response status and if it's not a success

    response (between 200 and 299), it rejects the promise.
    This operation will cause the promise chain to skip all the chained promises listed
    and will skip directly to the catch() statement at the bottom, logging the Request 
    failed text along with the error message.
    If that succeeds instead, it calls the json() function we defined. Since the 
    previous promise, when successful, returned the response object, we get it as an 
    input to the second promise. In this case, we return the data JSON processed, so the
    third promise receives the JSON directly:
        .then((data) => {
            console.log('Request succeeded with JSON response', data)
        })
    and we simply log it to the console.

5) Handling errors
    In the example, in the previous section, we had a catch that was appended to the chain of
    promises.
    When anything in the chain of promises fails and raises an error or rejects the promise, the
    control goes to the nearest catch() statement down the chain.
        ```
        new Promise((resolve, reject) => {
            throw new Error('Error')
        })
        .catch((err) => { console.error(err) })
        
        // or
        
        new Promise((resolve, reject) => {
            reject('Error')
        })
        .catch((err) => { console.error(err) })
        ```
6) Cascading errors
    If inside the catch() you raise an error, you can append a second catch() to handle it, and
    so on.
        ```
        new Promise((resolve, reject) => {
            throw new Error('Error')
        })
        .catch((err) => { throw new Error('Error') })
        .catch((err) => { console.error(err) })
        ```
7)  Orchestrating promises
    
    a) Promise.all()
        If you need to synchronize different promises, Promise.all() helps you define a list of
        promises, and execute something when they are all resolved.
        Example:
            ```
            const f1 = fetch('/something.json')
            const f2 = fetch('/something2.json')
            Promise.all([f1, f2]).then((res) => {
                console.log('Array of results', res)
            })
            .catch((err) => {
                console.error(err)
            })


            The ES2015 destructuring assignment syntax allows you to also do
            Promise.all([f1, f2]).then(([res1, res2]) => {
            console.log('Results', res1, res2)
            })
            ```
        You are not limited to using fetch of course, any promise is good to go.
    
    b) Promise.race()
        Promise.race() runs when the first of the promises you pass to it resolves, and it runs the
        attached callback just once, with the result of the first promise resolved.
        Example:
            ```
            const first = new Promise((resolve, reject) => {
                setTimeout(resolve, 500, 'first')
            })
            const second = new Promise((resolve, reject) => {
                setTimeout(resolve, 100, 'second')
            })
            Promise.race([first, second]).then((result) => {
                console.log(result) // second
            })
            ```
8)  Common errors
    Uncaught TypeError: undefined is not a promise
    If you get the Uncaught TypeError: undefined is not a promise error in the console, make sure
    you use new Promise() instead of just Promise()

                                Async/await

1) Prepending the async keyword to any function means that the function will return a promise
    This is why this code is valid:
        ```
        const aFunction = async () => {
            return 'test'
        }
        aFunction().then(alert) // This will alert 'test'
        
        and it's the same as:
        
        const aFunction = async () => {
            return Promise.resolve('test')
        }
        aFunction().then(alert) // This will alert 'test'
        ```

2)  Introduction
    JavaScript evolved in a very short time from callbacks to promises (ES2015), and since
    ES2017 asynchronous JavaScript is even simpler with the async/await syntax.
    Async functions are a combination of promises and generators, and basically, they are a
    higher level abstraction over promises. Let me repeat: async/await is built on promises.
    Why were async/await introduced?
    They reduce the boilerplate around promises, and the "don't break the chain" limitation of
    chaining promises.
    When Promises were introduced in ES2015, they were meant to solve a problem with
    asynchronous code, and they did, but over the 2 years that separated ES2015 and ES2017, it
    was clear that promises could not be the final solution.
    Promises were introduced to solve the famous callback hell problem, but they introduced
    complexity on their own, and syntax complexity.
    They were good primitives around which a better syntax could be exposed to the developers,
    so when the time was right we got async functions.
    They make the code look like it's synchronous, but it's asynchronous and non-blocking behind
    the scenes.
    
3) How it works
    An async function returns a promise, like in this example:
        ```
        const doSomethingAsync = () => {
            return new Promise((resolve) => {
                setTimeout(() => resolve('I did something'), 3000)
            })
        }
        ```
    When you want to call this function you prepend await , and the calling code will stop until
    the promise is resolved or rejected. One caveat: the client function must be defined as
    async . Here's an example:
        ```
        const doSomething = async () => {
            console.log(await doSomethingAsync())
        }
        ```
    A quick example
    This is a simple example of async/await used to run a function asynchronously:
        ```
        const doSomethingAsync = () => {
            return new Promise((resolve) => {
                setTimeout(() => resolve('I did something'), 3000)
            })
        }
        const doSomething = async () => {
            console.log(await doSomethingAsync())
        }
        console.log('Before')
        doSomething()
        console.log('After')
        
        The above code will print the following to the browser console:
        Before
        After
        I did something //after 3s
        ```
    
    Promise all the things
    
    Prepending the async keyword to any function means that the function will return a promise.
    Even if it's not doing so explicitly, it will internally make it return a promise.
    This is why this code is valid:
        ```
        const aFunction = async () => {
            return 'test'
        }
        ```
    `aFunction().then(alert) // This will alert 'test'
    and it's the same as:
    ```
    const aFunction = async () => {
        return Promise.resolve('test')
    }
    aFunction().then(alert) // This will alert 'test'
    ```
    The code is much simpler to read
    As you can see in the example above, our code looks very simple. Compare it to code using
    plain promises, with chaining and callback functions.
    And this is a very simple example, the major benefits will arise when the code is much more
    complex.

    For example here's how you would get a JSON resource, and parse it, using promises:
        ```
        const getFirstUserData = () => {
        return fetch('/users.json') // get users list
        .then(response => response.json()) // parse JSON
        .then(users => users[0]) // pick first user
        .then(user => fetch(`/users/${user.name}`)) // get user data
        .then(userResponse => response.json()) // parse JSON
        }
        getFirstUserData()
        ```

    And here is the same functionality provided using await/async:
        ```
        const getFirstUserData = async () => {
        const response = await fetch('/users.json') // get users list
        const users = await response.json() // parse JSON
        const user = users[0] // pick first user
        const userResponse = await fetch(`/users/${user.name}`) // get user data
        const userData = await user.json() // parse JSON
            return userData
        }
        getFirstUserData()
        ```
4) Multiple async functions in series
    Async functions can be chained very easily, and the syntax is much more readable than with
    plain promises:
        ```
        const promiseToDoSomething = () => {
            return new Promise(resolve => {
                setTimeout(() => resolve('I did something'), 10000)
            })
        }
        const watchOverSomeoneDoingSomething = async () => {
            const something = await promiseToDoSomething()
            return something + ' and I watched'
        }
        const watchOverSomeoneWatchingSomeoneDoingSomething = async () => {
            const something = await watchOverSomeoneDoingSomething()
            return something + ' and I watched as well'
        }
        watchOverSomeoneWatchingSomeoneDoingSomething().then((res) => {
            console.log(res)
        })
        ```
        
    Will print:
    I did something and I watched and I watched as well


5) Easier debugging
    Debugging promises is hard because the debugger will not step over asynchronous code.
    Async/await makes this very easy because to the compiler it's just like synchronous code.
   
   
   
                             The Node Event Emitter

1) How to work with custom events in Node
    If you worked with JavaScript in the browser, you know how much of the interaction of
    the user is handled through events: mouse clicks, keyboard button presses, reacting to mouse
    movements, and so on.
    On the backend side, Node offers us the option to build a similar system using the events
    module.
    This module, in particular, offers the EventEmitter class, which we'll use to handle
    our events.

    You initialize that using
    `const eventEmitter = require('events').EventEmitter()

    This object exposes, among many others, the on and emit methods.
    emit is used to trigger an event
   
    on is used to add a callback function that's going to be executed when the event is
    triggered

    For example, let's create a start event, and as a matter of providing a sample, we react to
    that by just logging to the console:
    ```
    eventEmitter.on('start', () => {
        console.log('started')
    })
    ```
    When we run
    `eventEmitter.emit('start')
    
    the event handler function is triggered, and we get the console log.
    You can pass arguments to the event handler by passing them as additional arguments to
    emit() :
    ```
    eventEmitter.on('start', (number) => {
        console.log(`started ${number}`)
    })
    ```

    eventEmitter.emit('start', 23)
   
2)  Multiple arguments:
    ```
    eventEmitter.on('start', (start, end) => {
        console.log(`started from ${start} to ${end}`)
    })
    eventEmitter.emit('start', 1, 100)
    ```
    
    The EventEmitter object also exposes several other methods to interact with events,
    like:-  
    once() : add a one-time listener  
    removeListener() / off() : remove an event listener from an event  
    removeAllListeners() : remove all listeners for an event  
    You can read all their details on the events module page at https://nodejs.org/api/  events.html  


                                HTTP

1) HTTP
    A detailed description of how the HTTP protocol, and the Web, work
    HTTP (Hyper Text Transfer Protocol) is one of the application protocols of TCP/IP, the suite of
    protocols that powers the Internet.
    Let me fix that: it's not one of the protocols, it's the most successful and popular one, by all
    means.
    HTTP is what makes the World Wide Web work, giving browsers a language to communicate
    to remote servers that host web pages.
    HTTP was first standardized in 1991, as a result of the work that Tim Berners-Lee did at
    CERN, the European Center of Nuclear Research, since 1989.
    The goal was to allow researchers to easily exchange and interlink their papers. It was meant
    as a way for the scientific community to work better.
    Back then the internet main applications basically consisted in FTP (the File Transfer
    Protocol), Email and Usenet (newsgroups, today almost abandoned).
    In 1993 Mosaic, the first graphical web browser, was released, and things skyrocketed from
    there.
    The Web became the killer app of the Internet.
    Over time the Web and the ecosystem around it have dramatically evolved, but the basics still
    remain. One example of evolution: HTTP now powers, in addition to web pages, REST APIs,
    one common way to programmatically access a service over the Internet.
    HTTP got a minor revision in 1997 with HTTP/1.1, and in 2015 its successor, HTTP/2, was
    standardized and it's now being implemented by the major Web Servers used across the
    globe.
    The HTTP protocol is considered insecure, just like any other protocol (SMTP, FTP..) not
    served over an encrypted connection. This is why there is a big push nowadays towards using
    HTTPS, which is HTTP served over TLS.
    That said, the building blocks of HTTP/2 and HTTPS have their roots in HTTP, and in this
    article I'll introduce how HTTP works.
    HTML documents
    HTTP
    117
    HTTP is the way web browsers like Chrome, Firefox, Edge and many others (also called
    clients from here on) communicate with web servers.
    The name Hyper Text Transfer Protocol derives from the need of transferring not just files, like
    in FTP - the "File Transfer Protocol", but hypertexts, which would be written using HTML, and
    then represented graphically by the browser with a nice presentation and interactive links.
    Links were the driving force that drove adoption, along with the ease of creation of new web
    pages.
    HTTP is what transfer those hypertext files (and as we'll see also images and other file types)
    over the network.
    Hyperlinks
    Inside a web browser, a document can point to another document using links.
    A link is composed by a first part that determines the protocol and the server address, either
    through a domain name or an IP.
    This part is not unique to HTTP, of course.
    Then there's the document part. Anything appended to the address part represents the
    document path.
    For example, this document address is https://flaviocopes.com/http/ :
    https is the protocol.
    flaviocopes.com is the domain name that points to my server
    /http/ is the document URL relative to the server root path.
    The path can be nested: https://flaviocopes.com/page/privacy/ and in this case the document
    URL is /page/privacy .
    The web server is responsible for interpreting the request and, once analyzed, serving the
    correct response.
    A request
    What's in a request?
    The first thing is the URL, which we've already seen before.
    When we enter an address and press enter in our browser, under the hoods the server sends
    to the correct IP address a request like this:
    HTTP
    118
    GET /a-page
    where /a-page is the URL you requested.
    The second thing is the HTTP method (also called verb).
    HTTP in the early days defined 3 of them:
    GET
    POST
    HEAD
    and HTTP/1.1 introduced
    PUT
    DELETE
    OPTIONS
    TRACE
    We'll see them in detail in a minute.
    The third thing that composes a request is a set of HTTP headers.
    Headers are a set of key: value pairs that are used to communicate to the server-specific
    information that is predefined, so the server can know what we mean.
    I described them in detail in the HTTP request headers list.
    Give that list a quick look. All of those headers are optional, except Host .
    HTTP methods
    GET
    GET is the most used method here. It's the one that's used when you type an URL in the
    browser address bar, or when you click a link.
    It asks the server to send the requested resource as a response.
    HEAD
    HEAD is just like GET, but tells the server to not send the response body back. Just the
    headers.
    HTTP
    119
    POST
    The client uses the POST method to send data to the server. It's typically used in forms, for
    example, but also when interacting with a REST API.
    PUT
    The PUT method is intended to create a resource at that specific URL, with the parameters
    passed in the request body. Mainly used in REST APIs
    DELETE
    The DELETE method is called against an URL to request deletion of that resource. Mainly
    used in REST APIs
    OPTIONS
    When a server receives an OPTIONS request it should send back the list of HTTP methods
    allowed for that specific URL.
    TRACE
    Returns back to the client the request that has been received. Used for debugging or
    diagnostic purposes.
    HTTP Client/Server communication
    HTTP, as most of the protocols that belong to the TCP/IP suite, is a stateless protocol.
    Servers have no idea what's the current state of the client. All they care about is that they get
    request and they need to fulfill them.
    Any prior request is meaningless in this context, and this makes it possible for a web server to
    be very fast, as there's less to process, and also it gives it bandwidth to handle a lot of
    concurrent requests.
    HTTP is also very lean, and communication is very fast in terms of overhead. This contrasts
    with the protocols that were the most used at the time HTTP was introduced: TCP and
    POP/SMTP, the mail protocols, which involve lots of handshaking and confirmations on the
    receiving ends.
    HTTP
    120
    Graphical browsers abstract all this communication, but we'll illustrate it here for learning
    purposes.
    A message is composed by a first line, which starts with the HTTP method, then contains the
    resource relative path, and the protocol version:
    GET /a-page HTTP/1.1
    After that, we need to add the HTTP request headers. As mentioned above, there are many
    headers, but the only mandatory one is Host :
    GET /a-page HTTP/1.1
    Host: flaviocopes.com
    How can you test this? Using telnet. This is a command-line tool that lets us connect to any
    server and send it commands.
    Open your terminal, and type telnet flaviocopes.com 80
    This will open a terminal, that tells you
    Trying 178.128.202.129...
    Connected to flaviocopes.com.
    Escape character is '^]'.
    You are connected to the Netlify web server that powers my blog. You can now type:
    GET /axios/ HTTP/1.1
    Host: flaviocopes.com
    and press enter on an empty line to fire the request.
    The response will be:
    HTTP/1.1 301 Moved Permanently
    Cache-Control: public, max-age=0, must-revalidate
    Content-Length: 46
    Content-Type: text/plain
    Date: Sun, 29 Jul 2018 14:07:07 GMT
    Location: https://flaviocopes.com/axios/
    Age: 0
    Connection: keep-alive
    Server: Netlify
    Redirecting to https://flaviocopes.com/axios/
    HTTP
    121
    See, this is an HTTP response we got back from the server. It's a 301 Moved Permanently
    request. See the HTTP status codes list to know more about the status codes.
    It basically tells us the resource has permanently moved to another location.
    Why? Because we connected to port 80, which is the default for HTTP, but on my server I set
    up an automatic redirection to HTTPS.
    The new location is specified in the Location HTTP response header.
    There are other headers, all described in the HTTP response headers list.
    In both the request and the response, an empty line separates the request header from the
    request body. The request body in this case contains the string
    Redirecting to https://flaviocopes.com/axios/
    which is 46 bytes long, as specified in the Content-Length header. It is shown in the browser
    when you open the page, while it automatically redirects you to the correct location.
    In this case we're using telnet, the low-level tool that we can use to connect to any server, so
    we can't have any kind of automatic redirect.
    Let's do this process again, now connecting to port 443, which is the default port of the HTTPS
    protocol. We can't use telnet because of the SSL handshake that must happen.
    Let's keep things simple and use curl , another command-line tool. We cannot directly type
    the HTTP request, but we'll see the response:
    curl -i https://flaviocopes.com/axios/
    this is what we'll get in return:
    HTTP/1.1 200 OK
    Cache-Control: public, max-age=0, must-revalidate
    Content-Type: text/html; charset=UTF-8
    Date: Sun, 29 Jul 2018 14:20:45 GMT
    Etag: "de3153d6eacef2299964de09db154b32-ssl"
    Strict-Transport-Security: max-age=31536000
    Age: 152
    Content-Length: 9797
    Connection: keep-alive
    Server: Netlify
    <!DOCTYPE html>
    <html prefix="og: http://ogp.me/ns#" lang="en">
    <head>
    <meta charset="utf-8">
    HTTP
    122
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>HTTP requests using Axios</title>
    ....
    I cut the response, but you can see that the HTML of the page is being returned now.
    Other resources
    An HTTP server will not just transfer HTML files, but typically it will also serve other files: CSS,
    JS, SVG, PNG, JPG, lots of different file types.
    This depends on the configuration.
    HTTP is perfectly capable of transferring those files as well, and the client will know about the
    file type, thus interpret them in the right way.
    This is how the web works: when an HTML page is retrieved by the browser, it's interpreted
    and any other resource it needs to display property (CSS, JavaScript, images..) is retrieved
    through additional HTTP requests to the same server.


                                HTTP Request


The HTTP protocol
        First, I mention HTTPS in particular because things are different from an HTTPS connection.
        I analyze URL requests only
        How HTTP Requests work
        124
        Modern browsers have the capability of knowing if the thing you wrote in the address bar is an
        actual URL or a search term, and they will use the default search engine if it's not a valid URL.
        I assume you type an actual URL.
        When you enter the URL and press enter, the browser first builds the full URL.
        If you just entered a domain, like flaviocopes.com , the browser by default will prepend
        HTTP:// to it, defaulting to the HTTP protocol.
        Things relate to macOS / Linux
        Just FYI. Windows might do some things slightly differently.
        DNS Lookup phase
        The browser starts the DNS lookup to get the server IP address.
        The domain name is a handy shortcut for us humans, but the internet is organized in such a
        way that computers can look up the exact location of a server through its IP address, which is
        a set of numbers like 222.324.3.1 (IPv4).
        First, it checks the DNS local cache, to see if the domain has already been resolved recently.
        Chrome has a handy DNS cache visualizer you can see at chrome://net-internals/#dns
        If nothing is found there, the browser uses the DNS resolver, using the gethostbyname POSIX
        system call to retrieve the host information.
        gethostbyname
        gethostbyname first looks in the local hosts file, which on macOS or Linux is located in
        /etc/hosts , to see if the system provides the information locally.
        If this does not give any information about the domain, the system makes a request to the
        DNS server.
        The address of the DNS server is stored in the system preferences.
        Those are 2 popular DNS servers:
        8.8.8.8 : the Google public DNS server
        1.1.1.1 : the CloudFlare DNS server
        Most people use the DNS server provided by their internet provider.
        How HTTP Requests work
        125
        The browser performs the DNS request using the UDP protocol.
        TCP and UDP are two of the foundational protocols of computer networking. They sit at the
        same conceptual level, but TCP is connection-oriented, while UDP is a connectionless
        protocol, more lightweight, used to send messages with little overhead.
        How the UDP request is performed is not in the scope of this tutorial
        The DNS server might have the domain IP in the cache. It not, it will ask the root DNS server.
        That's a system (composed of 13 actual servers, distributed across the planet) that drives the
        entire internet.
        The DNS server does not know the address of each and every domain name on the planet.
        What it knows is where the top-level DNS resolvers are.
        A top-level domain is the domain extension: .com , .it , .pizza and so on.
        Once the root DNS server receives the request, it forwards the request to that top-level
        domain (TLD) DNS server.
        Say you are looking for flaviocopes.com . The root domain DNS server returns the IP of the
        .com TLD server.
        Now our DNS resolver will cache the IP of that TLD server, so it does not have to ask the root
        DNS server again for it.
        The TLD DNS server will have the IP addresses of the authoritative Name Servers for the
        domain we are looking for.
        How? When you buy a domain, the domain registrar sends the appropriate TDL the
        name servers. When you update the name servers (for example, when you change the
        hosting provider), this information will be automatically updated by your domain registrar.
        Those are the DNS servers of the hosting provider. They are usually more than 1, to serve as
        backup.
        For example:
        ns1.dreamhost.com
        ns2.dreamhost.com
        ns3.dreamhost.com
        The DNS resolver starts with the first, and tries to ask the IP of the domain (with the
        subdomain, too) you are looking for.
        That is the ultimate source of truth for the IP address.
        How HTTP Requests work
        126
        Now that we have the IP address, we can go on in our journey.
        TCP request handshaking
        With the server IP address available, now the browser can initiate a TCP connection to that.
        A TCP connection requires a bit of handshaking before it can be fully initialized and you can
        start sending data.
        Once the connection is established, we can send the request
        Sending the request
        The request is a plain text document structured in a precise way determined by the
        communication protocol.
        It's composed of 3 parts:
        the request line
        the request header
        the request body
        The request line
        The request line sets, on a single line:
        the HTTP method
        the resource location
        the protocol version
        Example:
        GET / HTTP/1.1
        The request header
        The request header is a set of field: value pairs that set certain values.
        There are 2 mandatory fields, one of which is Host , and the other is Connection , while all the
        other fields are optional:
        Host: flaviocopes.com
        Connection: close
        How HTTP Requests work
        127
        Host indicates the domain name which we want to target, while Connection is always set to
        close unless the connection must be kept open.
        Some of the most used header fields are:
        Origin
        Accept
        Accept-Encoding
        Cookie
        Cache-Control
        Dnt
        but many more exist.
        The header part is terminated by a blank line.
        The request body
        The request body is optional, not used in GET requests but very much used in POST requests
        and sometimes in other verbs too, and it can contain data in JSON format.
        Since we're now analyzing a GET request, the body is blank and we'll not look more into it.
        The response
        Once the request is sent, the server processes it and sends back a response.
        The response starts with the status code and the status message. If the request is successful
        and returns a 200, it will start with:
        200 OK
        The request might return a different status code and message, like one of these:
        404 Not Found
        403 Forbidden
        301 Moved Permanently
        500 Internal Server Error
        304 Not Modified
        401 Unauthorized
        The response then contains a list of HTTP headers and the response body (which, since we're
        making the request in the browser, is going to be HTML)
        How HTTP Requests work
        128
        Parse the HTML
        The browser now has received the HTML and starts to parse it, and will repeat the exact same
        process we did not for all the resources required by the page:
        CSS files
        images
        the favicon
        JavaScript files
        ...
        How browsers render the page then is out of the scope, but it's important to understand that
        the process I described is not just for the HTML pages, but for any item that's served over
        HTTP


                            Create HTTP Server


1) How to build an HTTP server with Node.js
    Here is the HTTP web server we used as the Node Hello World application in the Node.js
    introduction
    const http = require('http')
    const port = 3000
    const server = http.createServer((req, res) => {
    res.statusCode = 200
    res.setHeader('Content-Type', 'text/plain')
    res.end('Hello World\n')
    })
    server.listen(port, () => {
    console.log(`Server running at http://${hostname}:${port}/`)
    })
    Let's analyze it briefly. We include the http module.
    We use the module to create an HTTP server.
    The server is set to listen on the specified port, 3000 . When the server is ready, the listen
    callback function is called.
    The callback function we pass is the one that's going to be executed upon every request that
    comes in. Whenever a new request is received, the request event is called, providing two
    objects: a request (an http.IncomingMessage object) and a response (an http.ServerResponse
    object).
    request provides the request details. Through it, we access the request headers and request
    data.
    response is used to populate the data we're going to return to the client.
    In this case with
    res.statusCode = 200
    we set the statusCode property to 200, to indicate a successful response.
    We also set the Content-Type header:
    Build an HTTP server
    130
    res.setHeader('Content-Type', 'text/plain')
    and we end close the response, adding the content as an argument to end() :
    res.end('Hello World\n')



                                Making HTTP Requests

    1) Making HTTP requests
    How to perform HTTP requests with Node.js using GET, POST, PUT and
    DELETE
    I use the term HTTP, but HTTPS is what should be used everywhere, therefore these
    examples use HTTPS instead of HTTP.
    Perform a GET Request
    const https = require('https')
    const options = {
    hostname: 'flaviocopes.com',
    port: 443,
    path: '/todos',
    method: 'GET'
    }
    const req = https.request(options, (res) => {
    console.log(`statusCode: ${res.statusCode}`)
    res.on('data', (d) => {
    process.stdout.write(d)
    })
    })
    req.on('error', (error) => {
    console.error(error)
    })
    req.end()
    Perform a POST Request
    const https = require('https')
    const data = JSON.stringify({
    todo: 'Buy the milk'
    })
    const options = {
    hostname: 'flaviocopes.com',
    port: 443,
    path: '/todos',
    method: 'POST',
    headers: {
    Making HTTP requests
    132
    'Content-Type': 'application/json',
    'Content-Length': data.length
    }
    }
    const req = https.request(options, (res) => {
    console.log(`statusCode: ${res.statusCode}`)
    res.on('data', (d) => {
    process.stdout.write(d)
    })
    })
    req.on('error', (error) => {
    console.error(error)
    })
    req.write(data)
    req.end()
    PUT and DELETE
    PUT and DELETE requests use the same POST request format, and just change the
    options.method value.


                            AXIOS

    1) Using Axios has quite a few advantages over the native Fetch API:
        ```
        supports older browsers (Fetch needs a polyfill)
        has a way to abort a request
        has a way to set a response timeout
        has built-in CSRF protection
        supports upload progress
        performs automatic JSON data transformation
        works in Node.js
        ```
        axios.get(),axios.post(),axios.put() ,delete etc...

        const getBreeds = async () => {
            try {
                return await axios.get('https://dog.ceo/api/breeds/list/all')
            } catch (error) {
                console.error(error)
            }
        }
        ```

                                Web Sockets

1) Websockets
    WebSockets are an alternative to HTTP communication in Web Applications.
    They offer a long lived, bidirectional communication channel between client
    and server.
    WebSockets are an alternative to HTTP communication in Web Applications.
    They offer a long lived, bidirectional communication channel between client and server.
    Once established, the channel is kept open, offering a very fast connection with low latency
    and overhead.
    Browser support for WebSockets
    WebSockets are supported by all modern browsers.
    Websockets
    139
    How WebSockets differ from HTTP
    HTTP is a very different protocol, and also a different way of communicate.
    HTTP is a request/response protocol: the server returns some data when the client requests it.
    With WebSockets:
    the server can send a message to the client without the client explicitly requesting
    something
    the client and the server can talk to each other simultaneously
    very little data overhead needs to be exchanged to send messages. This means a low
    latency communication.
    WebSockets are great for real-time and long-lived communications.
    HTTP is great for occasional data exchange and interactions initiated by the client.
    HTTP is much simpler to implement, while WebSockets require a bit more overhead.
    Secured WebSockets
    Always use the secure, encrypted protocol for WebSockets, wss:// .
    ws:// refers to the unsafe WebSockets version (the http:// of WebSockets), and should be
    avoided for obvious reasons.
    Create a new WebSockets connection
    const url = 'wss://myserver.com/something'
    const connection = new WebSocket(url)
    connection is a WebSocket object.
    When the connection is successfully established, the open event is fired.
    Listen for it by assigning a callback function to the onopen property of the connection object:
    connection.onopen = () => {
    //...
    }
    If there's any error, the onerror function callback is fired:
    Websockets
    140
    connection.onerror = error => {
    console.log(`WebSocket error: ${error}`)
    }
    Sending data to the server using WebSockets
    Once the connection is open, you can send data to the server.
    You can do so conveniently inside the onopen callback function:
    connection.onopen = () => {
    connection.send('hey')
    }
    Receiving data from the server using
    WebSockets
    Listen with a callback function on onmessage , which is called when the message event is
    received:
    connection.onmessage = e => {
    console.log(e.data)
    }
    Implement a WebSockets server in Node.js
    ws is a popular WebSockets library for Node.js.
    We'll use it to build a WebSockets server. It can also be used to implement a client, and use
    WebSockets to communicate between two backend services.
    Easily install it using
    yarn init
    yarn add ws
    The code you need to write is very little:
    const WebSocket = require('ws')
    const wss = new WebSocket.Server({ port: 8080 })
    Websockets
    141
    wss.on('connection', ws => {
    ws.on('message', message => {
    console.log(`Received message => ${message}`)
    })
    ws.send('ho!')
    })
    This code creates a new server on port 8080 (the default port for WebSockets), and adds a
    callback function when a connection is established, sending ho! to the client, and logging the
    messages it receives.
    See a live example on Glitch
    Here is a live example of a WebSockets server: https://glitch.com/edit/#!/flavio-websocketsserver-example
    Here is a WebSockets client that interacts with the server: https://glitch.com/edit/#!/flaviowebsockets-client-example


                                Streams

1) What are streams
    Streams are one of the fundamental concepts that power Node.js applications.
    They are a way to handle reading/writing files, network communications, or any kind of end-toend information exchange in an efficient way.
    Streams are not a concept unique to Node.js. They were introduced in the Unix operating
    system decades ago, and programs can interact with each other passing streams through the
    pipe operator ( | ).
    For example, in the traditional way, when you tell the program to read a file, the file is read into
    memory, from start to finish, and then you process it.
    Using streams you read it piece by piece, processing its content without keeping it all in
    memory.
    The Node.js stream module provides the foundation upon which all streaming APIs are build

    Streams-powered Node APIs
    Due to their advantages, many Node.js core modules provide native stream handling
    capabilities, most notably:
    process.stdin returns a stream connected to stdin
    process.stdout returns a stream connected to stdout
    process.stderr returns a stream connected to stderr
    fs.createReadStream() creates a readable stream to a file
    fs.createWriteStream() creates a writable stream to a file
    net.connect() initiates a stream-based connection
    http.request() returns an instance of the http.ClientRequest class, which is a writable
    stream
    zlib.createGzip() compress data using gzip (a compression algorithm) into a stream
    zlib.createGunzip() decompress a gzip stream.
    zlib.createDeflate() compress data using deflate (a compression algorithm) into a
    stream
    zlib.createInflate() decompress a deflate stream
    Different types of streams
    There are four classes of streams:
    Readable : a stream you can pipe from, but not pipe into (you can receive data, but not
    send data to it). When you push data into a readable stream, it is buffered, until a
    consumer starts to read the data.
    Writable : a stream you can pipe into, but not pipe from (you can send data, but not
    Streams
    180
    receive from it)
    Duplex : a stream you can both pipe into and pipe from, basically a combination of a
    Readable and Writable stream
    Transform : a Transform stream is similar to a Duplex, but the output is a transform of its
    input
    

                                Working with MySQL

1)  MySQL is one of the most popular relational databases in the world. Find out
    how to make it work with Node.js
    MySQL is one of the most popular relational databases in the world.
    The Node ecosystem of course has several different packages that allow you to interface with
    MySQL, store data, retrieve data, and so on.
    We'll use mysqljs/mysql , a package that has over 12.000 GitHub stars and has been around
    for years.
    Installing the Node mysql package
    You install it using
    npm install mysql
    Initializing the connection to the database
    You first include the package:
    const mysql = require('mysql')
    and you create a connection:
    const options = {
    user: 'the_mysql_user_name',
    password: 'the_mysql_user_password',
    database: 'the_mysql_database_name'
    }
    const connection = mysql.createConnection(options)
    You initiate a new connection by calling:
    connection.connect(err => {
    if (err) {
    console.error('An error occurred while connecting to the DB')
    throw err
    }
    })
    Working with MySQL
    184
    The connection options
    In the above example, the options object contained 3 options:
    const options = {
    user: 'the_mysql_user_name',
    password: 'the_mysql_user_password',
    database: 'the_mysql_database_name'
    }
    There are many more you can use, including:
    host , the database hostname, defaults to localhost
    port , the MySQL server port number, defaults to 3306
    socketPath , used to specify a unix socket instead of host and port
    debug , by default disabled, can be used for debugging
    trace , by default enabled, prints stack traces when errors occur
    ssl , used to setup an SSL connection to the server (out of the scope of this tutorial)
    Perform a SELECT query
    Now you are ready to perform an SQL query on the database. The query once executed will
    invoke a callback function which contains an eventual error, the results and the fields.
    connection.query('SELECT * FROM todos', (error, todos, fields) => {
    if (error) {
    console.error('An error occurred while executing the query')
    throw error
    }
    console.log(todos)
    })
    You can pass in values which will be automatically escaped:
    const id = 223
    connection.query('SELECT * FROM todos WHERE id = ?', [id], (error, todos, fields) => {
    if (error) {
    console.error('An error occurred while executing the query')
    throw error
    }
    console.log(todos)
    })
    Working with MySQL
    185
    To pass multiple values, just put more elements in the array you pass as the second
    parameter:
    const id = 223
    const author = 'Flavio'
    connection.query('SELECT * FROM todos WHERE id = ? AND author = ?', [id, author], (error,
    todos, fields) => {
    if (error) {
    console.error('An error occurred while executing the query')
    throw error
    }
    console.log(todos)
    })
    Perform an INSERT query
    You can pass an object
    const todo = {
    thing: 'Buy the milk'
    author: 'Flavio'
    }
    connection.query('INSERT INTO todos SET ?', todo, (error, results, fields) => {
    if (error) {
    console.error('An error occurred while executing the query')
    throw error
    }
    })
    If the table has a primary key with auto_increment , the value of that will be returned in the
    results.insertId value:
    const todo = {
    thing: 'Buy the milk'
    author: 'Flavio'
    }
    connection.query('INSERT INTO todos SET ?', todo, (error, results, fields) => {
    if (error) {
    console.error('An error occurred while executing the query')
    throw error
    }}
    const id = results.resultId
    console.log(id)
    )
    Close the connection
    Working with MySQL
    186
    When you need to terminate the connection to the database you can call the end() method:
    connection.end()
    This makes sure any pending query gets sent, and the connection is gracefully terminated.

                            Important Modules
1) https
2) os
3) fs
