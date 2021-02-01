# ca-promises-js

node app.js

##### Constructing a Promise Object
Let’s construct a promise! To create a new Promise object, we use the new keyword and the Promise constructor method:
>const executorFunction = (resolve, reject) => { };
>const myFirstPromise = new Promise(executorFunction);
The Promise constructor method takes a function parameter 
called the executor function which runs automatically when the constructor is called. 
The executor function generally starts an asynchronous operation and dictates how the promise should be settled.
1) view code here:
https://gist.github.com/ad378564d8d6f7bec03afda4b28db698

##### The Node setTimeout() Function
Knowing how to construct a promise is useful, but most of the time, knowing how to consume, or use, promises will be key. Rather than constructing promises, you’ll be handling Promise objects returned to you as the result of an asynchronous operation. These promises will start off pending but settle eventually.
Moving forward, we’ll be simulating this by providing you with functions that return promises which settle after some time. To accomplish this, we’ll be using setTimeout(). setTimeout() is a Node API (a comparable API is provided by web browsers) that uses callback functions to schedule tasks to be performed after a delay. setTimeout() has two parameters: a callback function and a delay in milliseconds.  Invoke setTimeout() with the callback function delayedHello() and 2000. In at least two seconds delayedHello() will be invoked. But why is it “at least” two seconds and not exactly two seconds?
This delay is performed asynchronously—the rest of our program won’t stop executing during the delay. Asynchronous JavaScript uses something called the event-loop. After two seconds, delayedHello() is added to a line of code waiting to be run. Before it can run, any synchronous code from the program will run. Next, any code in front of it in the line will run. This means it might be more than two seconds before delayedHello() is actually executed.
Let us use setTimeout() to construct asynchronous promises:
2) view code here:
https://gist.github.com/2bfc547329b80f07963d24622680df1b

##### Consuming Promises
The initial state of an asynchronous promise is pending, but we have a guarantee that it will settle. How do we tell the computer what should happen then? Promise objects come with an aptly named .then() method. It allows us to say, “I have a promise, when it settles, then here’s what I want to happen…”
In the case of our dishwasher promise, the dishwasher will run then:
If our promise rejects, this means we have dirty dishes, and we’ll add soap and run the dishwasher again.
If our promise fulfills, this means we have clean dishes, and we’ll put the dishes away.
.then() is a higher-order function— it takes two callback functions as arguments. We refer to these callbacks as handlers. When the promise settles, the appropriate handler will be invoked with that settled value.  The first handler, sometimes called onFulfilled, is a success handler, and it should contain the logic for the promise resolving.  The second handler, sometimes called onRejected, is a failure handler, and it should contain the logic for the promise rejecting.  We can invoke .then() with one, both, or neither handler! This allows for flexibility, but it can also make for tricky debugging. If the appropriate handler is not provided, instead of throwing an error, .then() will just return a promise with the same settled value as the promise it was called on. One important feature of .then() is that it always returns a promise. We’ll return to this in more detail in a later exercise and explore why it’s so important.
##### The onFulfilled and onRejected Functions
To handle a “successful” promise, or a promise that resolved, we invoke .then() on the promise, passing in a success handler callback function:  https://gist.github.com/66b2d140a244044ffe756c5907a77a71

##### Using catch() with Promises
One way to write cleaner code is to follow a principle called separation of concerns. Separation of concerns means organizing code into distinct sections each handling a specific task. It enables us to quickly navigate our code and know where to look if something isn’t working.
Remember, .then() will return a promise with the same settled value as the promise it was called on if no appropriate handler was provided. This implementation allows us to separate our resolved logic from our rejected logic. Instead of passing both handlers into one .then(), we can chain a second .then() with a failure handler to a first .then() with a success handler and both cases will be handled.

>prom
>  .then((resolvedValue) => {
>    console.log(resolvedValue);
>  })
>  .then(null, (rejectionReason) => {
>    console.log(rejectionReason);
>  });

Since JavaScript doesn’t mind whitespace, we follow a common convention of putting each part of this chain on a new line to make it easier to read. To create even more readable code, we can use a different promise function: .catch().
The .catch() function takes only one argument, onRejected. In the case of a rejected promise, this failure handler will be invoked with the reason for rejection. Using .catch() accomplishes the same thing as using a .then() with only a failure handler.

Example using: .catch():
>prom
>  .then((resolvedValue) => {
>    console.log(resolvedValue);
>  })
>  .catch((rejectionReason) => {
>   console.log(rejectionReason);
>  });

A break down what’s happening in the example code:
prom is a promise which randomly either resolves with 'Yay!' or rejects with 'Ohhh noooo!'.
We pass a success handler to .then() and a failure handler to .catch().
If the promise resolves, .then()‘s success handler will be invoked with 'Yay!'.
If the promise rejects, .then() will return a promise with the same rejection reason as the original promise and .catch()‘s failure handler will be invoked with that rejection reason.
Let’s practice writing .catch() functions.
7) view code here:
https://gist.github.com/a14412435085658ba1c19d761cea70e5




