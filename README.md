# renovate-config

This is the repo for our `default` implementation of renovate.json.

If most/all repo's extend this, then things like the npmtoken (necessary for updating some @luxuryescapes npm dependencies) can be
updated here and have that propagate to most repos.

# Config
```json
{
  "dependencyDashboard": true,
  "encrypted": { //the token/s inside must have been encrypted by renovates public key, so only renovate can use them
                 //https://docs.renovatebot.com/getting-started/private-packages/#add-an-encrypted-npm-token-to-renovate-config
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
  "prCreation": "not-pending", //wait until CI has finished to raise PR (fail or pass)
  "prNotPendingHours": 24, //if CI has not finished after 24 hours, raise PR anyway
  "rangeStrategy": "replace", //Replace the range with a newer one if the new version falls outside it, and update nothing otherwise
  "separateMultipleMajor": true //PRs will be raised separately for each available major upgrade version.
}
```
