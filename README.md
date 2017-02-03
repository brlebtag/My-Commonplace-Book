# Metal Notes

- When you use an external library or a very tested algorithm and your code relies on it to work but it isn't working,
you are probably using it **wrong** or there is a **logical problem** in your code. Programmer always will blame someone'else code
instead of his own.
- Be careful with Java's **finally** or Ruby's **ensure** operations. you may forget they will always be executed regardless of execeptions (that's the point anyway). Those operations are usually use to clean or release resources but sometimes they shouldn't be clean or you're arraging the command wrongly.