# renovate-config

This is the repo for our `default` implementation of renovate.json.

If most/all repo's extend this, then things like the npmtoken (necessary for updating some @luxuryescapes npm dependencies) can be
updated here and have that propagate to most repos.

# Config

Consult the [Docs](https://docs.renovatebot.com/configuration-options/).

```json
{
  "dependencyDashboard": true,
  //the token/s inside must have been encrypted by renovates public key,
  //so only renovate can use them
  //original key is the production npm token found on customer portal on heroku
  //https://docs.renovatebot.com/getting-started/private-packages/#add-an-encrypted-npm-token-to-renovate-config
  "encrypted": {
    "npmToken": "encrypted token"
  },
  "npmrc": "//registry.npmjs.org/:_authToken=${NPM_TOKEN}",
  "packageRules": [
    {
      "groupName": "dev-dependencies",
      "matchDepTypes": ["devDependencies"]
    },
    {
      "groupName": "luxuryescapes-packages",
      "matchPackagePrefixes": ["@luxuryescapes/"]
    },
    {
      "groupName": "minor-packages",
      "matchUpdateTypes": ["digest", "minor", "patch", "pin"],
      "excludeDepNames": [
        "node"
      ]
    },
    {
      "groupName": "Node",
      "matchPackageNames": ["cimg/node", "node"]
    }
  ],
  "prConcurrentLimit": 5,
  //wait until CI has finished to raise PR (fail or pass)
  "prCreation": "not-pending",
  //if CI has not finished after 24 hours, raise PR anyway
  "prNotPendingHours": 24,
  //Replace the range with a newer one if the new version falls outside it, and update nothing otherwise
  "rangeStrategy": "replace",
  //PRs will be raised separately for each available major upgrade version.
  "separateMultipleMajor": true
}
```
