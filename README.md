# Mental Notes

## General rules
- When you're using an external library or a very well tested algorithm and your code relies on it to work but it isn't, you are probably using it in the **wrong** way or there is a **logical problem** in your code. Programmers always tend to blame someone'else code instead of his own.

- Watch for Java's **finally** or Ruby's **ensure** operations, or any other **finallyish** function and what you're releasing. Not everything should be released or it's suitable to be released in that moment (e.g. mutex for a bigger or complex operation).

## GIT

- Always lock the master branch, preventing it from direct push or forced push. Use pull request and new commits instead.

## Postgresql
- Don't forget to **sort the row_col column** if you're using postgres's **crosstab**.
