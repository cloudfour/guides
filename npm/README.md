# Working with C4 Pattern Libraries

TODO - fill in here

## Publishing a new version

Prerequisites: [Node](https://nodejs.org) with NPM version 5.7.0+ (required for `npm ci` to work)

If you haven't already set yourself up for NPM publishing, you need to do the following:

- Either confirm that you have an NPM account or create one (you'll need your username and password)
- Confirm you have set up two-factor authentication on your NPM account or set it up
  - Set up 2FA to protect `Authorization and Publishing`
- Use a phone app to complete your 2FA setup, scanning the QR code offered to you
  - This app will now provide you with a One-Time Password (OTP), every time you do a task that requires 2FA

- Login to the C4 NPM account (see 1Password for details: `cloudfour-user`)
- Go to the account settings for `cloudfour` (not `cloudfour-user`), under `Organizations`
- Go to the `Members` tab and use `Invite Members` to invite yourself, using the NPM username you had or just created
- You may or may not need to logout and go to your account to accept the invite

Now you are ready to version and publish your package

- In the terminal, type `npm adduser <your_user_name>`
  - At the following prompts enter
  - Your username
  - Your password
  - Your email address
  - A new OTP from your phone, once prompted

When you see your user is set up to publish, you can now do the following

- `npm version <new version here>`
  - Refer to the previous version and follow [Semver](https://docs.npmjs.com/getting-started/semantic-versioning)
  - For example, a basic, non breaking update for version `1.0.0` would be `npm version 1.1.0`

- `git add . && git commit -m "Note about versioning patterns"`

Now is the time to merge your PR to `master`, once approved

- On `master`, **_AFTER_** merging the PR, **_NOT_** in your branch: `npm publish`
