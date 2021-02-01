# ca-promises-js

##### Constructing a Promise Object
Let’s construct a promise! To create a new Promise object, we use the new keyword and the Promise constructor method:
>const executorFunction = (resolve, reject) => { };
>const myFirstPromise = new Promise(executorFunction);
The Promise constructor method takes a function parameter 
called the executor function which runs automatically when the constructor is called. 
The executor function generally starts an asynchronous operation and dictates how the promise should be settled.
1) view code here:
https://gist.github.com/ad378564d8d6f7bec03afda4b28db698
