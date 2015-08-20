# OAuth2

In the HSCS.io API, OAuth2 serves as a protocol that allows CTF organizers to get information about their participants through the HSCS.io infrastructure without explicitly getting identification materials such as their email or password.

In order to begin using the API's OAuth2 features as a CTF organizer, you must first register your CTF through the CTF application form. When you register your CTF, you will receive a unique Client ID and a Client Secret. For security purposes, do not publicly reveal your Client Secret. The Client Secret will only be shown to you once, and if you think your Secret has been compromised, you may choose to generate a new ID and Secret.

## Authentication Flow

Please follow these steps in authenticating users.

### Authorization

The first step in setting up OAuth2 is to have them sign in to their HSCS.io account. To do this, redirect them to the following page:

    https://hscs.io/api/oauth/authorize

Supply the following parameters:

- `client_id` (required): The Client ID you were issued when you registered the CTF.
- `redirect_uri` (required): One of the Redirect URIs that you chose when you registered the CTF.
- `scope` (optional): One of the following scopes that grants your CTF their respective permissions. Should multiple scopes be requested, they must be separated by commas.
    - `read`: Allows the CTF to read information about the user
    - `write`: Allows the CTF to post and write information about the user
