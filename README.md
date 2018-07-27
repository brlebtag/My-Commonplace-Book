# Mental Notes

## General rules
- When you're using an external library or a very well tested algorithm and your code relies on it to work but it isn't, you are probably using it in the **wrong** way or there is a **logical problem** in your code. Programmers always tend to blame someone'else code instead of his own.

- Watch for Java's **finally** or Ruby's **ensure** operations, or any other **finallyish** function and what you're releasing. Not everything should be released or it's suitable to be released in that moment (e.g. mutex for a bigger or complex operation).

## GIT

- Always lock the master branch, preventing it from direct push or forced push. Use pull request and new commits instead.

## Postgresql
- Don't forget to **sort the row_col column** if you're using postgres's **crosstab**.
- `SELECT 'infinity'::DATE` is the biggest date ever in postgres.

## Access control System design
- DO NOT FORGET THIS SCENARIO: Imagine you're implementing an access control system and you set permissions in all CRUD actions. Now, imagine you have the following situation:
User A can't list categories (they don't have access to list categories screen), but User A can access post creation screen and in post creation screen there is a list of categories. They don't have direct access to list categories but can list categories in post creation screen.