# OAuth2

In the HSCS.io API, OAuth2 serves as a protocol that allows CTF organizers to get information about their participants through the HSCS.io infrastructure without explicitly getting identification materials such as their email or password.

In order to begin using the API's OAuth2 features as a CTF organizer, you must first register your CTF through the CTF application form. When you register your CTF, you will receive a unique Client ID and a Client Secret. For security purposes, do not publicly reveal your Client Secret. The Client Secret will only be shown to you once, and if you think your Secret has been compromised, you may choose to generate a new ID and Secret.

## Authentication Flow

Please follow these steps in authenticating users.

### Authorization

The first step in setting up OAuth2 is to have them sign in to their HSCS.io account. To do this, redirect them to the following page:

```
https://hscs.io/api/oauth/authorize
```

Supply the following parameters:

- `client_id` (required): The Client ID you were issued when you registered the CTF.
- `redirect_uri` (required): One of the Redirect URIs that you chose when you registered the CTF.
- `scope` (optional): One of the following scopes that grants your CTF their respective permissions. Should multiple scopes be requested, they must be separated by commas.
    - `read`: Allows the CTF to read information about the user
    - `write`: Allows the CTF to post and write information about the user

Should a user grant your CTF permissions, the user will be redirected to the `redirect_uri` along with a GET parameter named `code`, which contains a temporary code you can use to exchange for an access token. Should a user deny your request to access their account, the user will be redirected to the `redirect_uri` along with a GET parameter named `error`, which contains something like `access_denied`.

### Token Issuing

When the users sign into their HSCS.io accounts and grant your CTF permission to access their information, you will receive a temporary code which you can trade for an access token. The temporary code is passed as a GET parameter called `code` when they are redirected to the `redirect_uri` you supplied. The exchange of code for access token must be done from server to server, so the Client Secret is never revealed to the user.

To receive an access token, send a POST request to the following url:

```
https://hscs.io/api/oauth/access_token
```

Supply the following parameters:

- `client_id` (required): The Client ID you were issued when you registered the CTF.
- `client_secret` (required): The Client Secret you were issued when you registered the CTF.
- `code` (required): The temporary code you were issued when the user granted permissions.
- `redirect_uri` (required): The same redirect_uri that you redirected the user with.

You will receive a JSON response with the following information:

- `access_token`: The access token you can use to make API calls on the user’s behalf.
- `scope`: The scope that was granted to you by the user. This will match the scope you originally provided.

Once you’ve received an access token, you can use the access token to make API calls, and you will not need to use this authentication process again. Although these access tokens do not expire automatically, note that users can revoke your access token at any time through their control panel.