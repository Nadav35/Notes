## The Event Loop in JavaScript
* Javascript has a callstack, `event loop`, callback queue
* Javascript runtime is a heap
* Callstack is where the stackframes live
* Event loop and callback queue
* The call stack
  * JS is a single threaded programming language (it can only run one thing at a time)
    * In ruby many things can happen at once (It is a threaded language)
  * The call stack is a data structure that records where in the program we are, we can push on to the stack and pop off the stack
  * A good example to use when explaining the callstack is a setTimeout(() => console.log("hi"), 500)
    * The console log get's added to the callstack and is not popped off of the call stack until a half a second has passed.