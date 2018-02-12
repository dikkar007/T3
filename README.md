

JavaScript and python. It is tedious, complicated, but gets the job done.

When the request come to server


Even though V8 is single-threaded, the underlying C++ API of Node isn't. It means that whenever we call something that is a non-blocking operation, Node will call some code that will run concurrently with our javascript code under the hood. Once this hiding thread receives the value it awaits for or throws an error, the provided callback will be called with the necessary parameters.

Task queue

Javascript is a single-threaded, event-driven language. This means that we can attach listeners to events, and when a said event fires, the listener executes the callback we provided.

Whenever you call setTimeout, http.get or fs.readFile, Node.js sends these operations to a different thread allowing V8 to keep executing our code. Node also calls the callback when the counter has run down or the IO / http operation has finished.

These callbacks can enqueue other tasks and those functions can enqueue others and so on. This way you can read a file while processing a request in your server, and then make an http call based on the read contents without blocking other requests from being handled.

However, we only have one main thread and one call-stack, so in case there is another request being served when the said file is read, its callback will need to wait for the stack to become empty. The limbo where callbacks are waiting for their turn to be executed is called the task queue (or event queue, or message queue). Callbacks are being called in an infinite loop whenever the main thread has finished its previous task, hence the name 'event loop'.

Microtasks and Macrotasks
The event loop might be a slippery concept to grasp at first, but once you get the hang of it, you won't be able to imagine that there is life without it

What is the Event Loop?

The event loop is what allows Node.js to perform non-blocking I/O operations — despite the fact that JavaScript is single-threaded — by offloading operations to the system kernel whenever possible.

Since most modern kernels are multi-threaded, they can handle multiple operations executing in the background. When one of these operations completes, the kernel tells Node.js so that the appropriate callback may be added to the poll queue to eventually be executed. 


Docker Enables Consistent Environments


Sharing your environment with your team

One of the harder parts of a team working together on an application using the same codebase is standardizing everyone’s development environment. Tools like Git and GitHub have solved the problem of teams sharing the code itself, but prior to containers, many teams used a series of shell scripts to try to configure each other’s machines as closely as possible, or even just instructions in a README file. By creating and sharing Dockerfiles and images with your team, it’s much easier to make sure everyone is working with the same base, and you’ll be free to focus your energy on development time instead of worrying about fixing configuration problems across your team’s computers.

Deploying your application

Making your application run on your own computer is a huge accomplishment, but as applications get more and more complex, getting your local environment to match up with a production environment on a server can get tricky. Docker can help here too. If your local environment is just Docker running containers, then if you can get Docker running on your production server, those same containers should work there too. 







# T3


