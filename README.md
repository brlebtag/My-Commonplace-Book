# Mental Notes

## General rules
- When you use an external library or a very well tested algorithm and your code relies on it to work but it isn't working,
you are probably using it **wrong** or there is a **logical problem** in your code. Programmer always will blame someone'else code
instead of his own.
- Watch for Java's **finally** or Ruby's **ensure** operations, or any other **finallyish** function and what you're releasing. Not everything should be released.

## GIT

- Always lock the master branch, preventing it from direct push or forced push. Use pull request and new commits instead.

## Postgresql
- Don't forget to sort the row_col column if you're using postgres's crosstab.
