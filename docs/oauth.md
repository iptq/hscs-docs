# OAuth2

In the HSCS.io API, OAuth2 serves as a protocol that allows CTF organizers to get information about their participants through the HSCS.io infrastructure without explicitly getting identification materials such as their email or password.

In order to begin using the API's OAuth2 features as a CTF organizer, you must first register your CTF through the CTF application form. When you register your CTF, you will receive a unique Client ID and a Client Secret. For security purposes, do not publicly reveal your Client Secret. The Client Secret will only be shown to you once, and if you think your Secret has been compromised, you may choose to generate a new ID and Secret.

## Authentication Flow

Please follow these steps in authenticating users.