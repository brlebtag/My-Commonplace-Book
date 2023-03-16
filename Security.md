[< Back](https://github.com/brlebtag/My-Commonplace-Book)

# Security

## Access control System design
- DO NOT FORGET THIS SCENARIO: Imagine you're implementing an access control system and you set permissions in all CRUD actions. Now, imagine you have the following situation:
_User A_ can't list categories (they don't have access to list categories screen), but _User A_ can access post creation screen and in post creation screen there is a list of categories. They don't have direct access to list categories but can list categories in post creation screen.
