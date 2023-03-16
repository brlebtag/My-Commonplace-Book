# General and Useful observations from my experience or observed in others

- When you're using an external library or a very well tested algorithm and your code relies on it to work but it isn't, you are probably using it in the **wrong** way or there is a **logical problem** in your code. Programmers always tend to blame someone'else code instead of their own.

- Watch out for Java's **finally** or Ruby's **ensure** operations, or any other **finallyish** function and what you're releasing. Not everything should be released or it is suitable to be released in that moment. Although it is the right place to do such a thing, you may want to use that resource somewhere else yet and you have forgotten that you have released the resource.

- Be careful with async/await in a monothread model. Just because they are not running parallely doesn't mean someone else can't change your values.

- Never underestimate the possibility of an IO operation failure. Any kind of IO operation can and eventually will fail, no matter how odd the chances are.
