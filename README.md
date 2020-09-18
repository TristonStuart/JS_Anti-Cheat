# JS_Anti-Cheat
Collection of some javascript anti-cheat methods

## Detect Function Hooking and Code Changes with Error Stacks
#### Found by Triston Stuart
(Note: You have to force a "natural" error. If you call an error, people can just hook the Error class. "natural" errors are not tied to the Error class so you can safely check the stack without worrying about it being modified.)
### Basic Explanation
Well, when you use global/default functions or methods any can hook into that function. They can then get the object the function was called on, get parameters that were passed, or go back through the call stack and get parameters from previously called functions. <br>
To deal with this you need to check either check global/default functions that could be hooked to access sensitive data (for example a player list array that uses the .push method to add new players), or check all global / default functions you use. 
<br>
<br>
The problem with this approach is that you have to get the exact right stack for each function and have it in your code. This is a very hard task, and makes updating code impossible as the stacks will change. To get around this I recommend getting the error stack for `String.prototype.match`, then you don't have to worry about code updating as you are just looking for a regex match. As long as you have the code that checks the `match` function at the top you don't have to worry about updating the code below it. 
