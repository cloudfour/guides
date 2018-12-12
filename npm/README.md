# Setting up your computer to publish to npm (only necessary the first time)

Prerequisites: [Node.js](https://github.com/creationix/nvm#installation) with npm version 5.7.0+ (required for `npm ci` to work)

## Setting up your npm account online

- [Either confirm that you have an npm account or create one](https://www.npmjs.com/) (you'll need your username and password)
- Confirm you have set up two-factor authentication on your npm account or set it up
  - Set up 2FA to protect `Authorization and Publishing`
- Use a 2FA provider to complete your 2FA setup ([1Password](https://1password.com/) or [Authy](https://authy.com/) or [Google Authenticator](https://itunes.apple.com/us/app/google-authenticator/id388497605?mt=8))
  - This app will now provide you with a One-Time Password (OTP), every time you do a task that requires 2FA
- Login to the C4 npm account (see 1Password for details: `cloudfour-user`)
- Go to the account settings for the `cloudfour` npm organization (not `cloudfour-user`)
- Go to the `Members` tab and use `Invite Members` to invite yourself, using the npm username you had or just created
- You may or may not need to logout and go to your account to accept the invite

## Signing in to npm locally

- In the terminal, type `npm adduser <your_user_name>`, and enter:
  - Your username
  - Your password
  - Your email address
  - A new OTP from your phone, once prompted

Once you are signed in, you should be ready to publish (see individual repos for per-repo publishing instructions)
