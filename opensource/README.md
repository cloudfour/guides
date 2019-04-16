# Open Source at Cloud Four

This guide is about how we manage our open-source work at Cloud Four. Given that this work happens across several Git repos that have been set up by various people over many years, it makes sense to have a guide that documents our current best thinking about how to operate them.

## NPM Package Setup

!!! THIS IS A WORK-IN-PROGRESS !!!

For open-source work that is published to npm, we need to do our due diligence. That includes ensuring that the package has tests, the build passes, there are no security vulnerabilities, and it stays up-to-date with dependencies.

- [@cloudfour npm packages](https://www.npmjs.com/org/cloudfour)

### Checklist

- [ ] one
- [ ] two
- [ ] three

### README file

Add note about recommended README bits:

- npm badge
- build status badge
- install instructions (from npm)
- link to documentation
- link to changelog

### CHANGELOG file

Add note about the importance of maintaining a changelog.

### Release Process

Add note about version bump and npm release process

- [bump](https://github.com/fabiospampinato/bump)

### Tests & Linting

Add note about testing and linting

### Continuous Integration

Add note about Travis (and .com/.org) to run tests and lint

### Automated Dependency Updates

Add note about Renovate

- How to evaluate Renovate PRs

### Automated Security Checks

Add note about Snyk

- Added by Jason in April 2017. Company was started by a friend of his, and some good people work there.
- How to evaluate Snyk security patches
- Lifecycle of a Snyk security patch

- [Snyk documentation](https://snyk.io/docs/)
- [Using Snyk, NSP and Retire.JS to Identify and Fix Vulnerable Dependencies in your Node.js Applications](https://developers.redhat.com/blog/2017/04/12/using-snyk-nsp-and-retire-js-to-identify-and-fix-vulnerable-dependencies-in-your-node-js-applications/)
- [NSP is shutting down](https://blog.npmjs.org/post/175511531085/the-node-security-platform-service-is-shutting)
- [Introducing `npm audit`: Identify and fix insecure dependencies](https://blog.npmjs.org/post/173719309445/npm-audit-identify-and-fix-insecure)
- [Difference between Snyk and NSP?](https://github.com/Snyk/snyk/issues/19)
- [Audit CI](https://www.npmjs.com/package/audit-ci)
- [Comparing NPM Audit with Synk](https://www.nearform.com/blog/comparing-npm-audit-with-snyk/)
- [Snyk demo app](https://github.com/snyk/snyk-demo-app)
- [Twitter thread about Snyk patches](https://twitter.com/spaceninja/status/1118179340871553024)
