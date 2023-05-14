# npmtoken

All repos with renovate should extend npmtoken.json. Thus we will have a single source of truth to update
across all repos.

Token taken from production customer portal on heroku.

# renovate-config

This is the repo for our `default` implementation of renovate.json. Repos without special needs should extend this.

# default.json Config

Consult the [Docs](https://docs.renovatebot.com/configuration-options/).

```json
{
  "dependencyDashboard": true,
  //extends the npmtoken config, the single source of truth for the npm token
  //"encrypted": {
  //  "npmToken": "encrypted_token"
  //}
  //encrypted_token is the customer portal production token from heroku
  //it is encrypted by renovate's public key
  //https://docs.renovatebot.com/getting-started/private-packages/#add-npmrc-string-to-renovate-config
  "extends": ["local>renovate-config:npmtoken"]
  "npmrc": "//registry.npmjs.org/:_authToken=${NPM_TOKEN}",
  "packageRules": [
    {
      "groupName": "dev-dependencies",
      "matchDepTypes": ["devDependencies"],
      "excludePackagePrefixes": ["@luxuryescapes/"],
      //later versions of chromedriver break e2e's. Manual updates only
      "excludePackageNames": ["chromedriver"]
    },
    {
      "groupName": "luxuryescapes-packages",
      "matchPackagePrefixes": ["@luxuryescapes/"]
    },
    {
      //added because yarn causes a lot of failures - updating it by itself makes updating packages easier
      "groupName": "Yarn",
      "matchPackageNames": ["yarn"]
    },
    {
      "groupName": "minor-packages",
      //will not update pinned versions - if you need a certain version then pin it
      "matchUpdateTypes": ["digest", "minor", "patch"],
      "excludePackageNames": ["node", "cimg/node", "@types/node", "chromedriver", "yarn"],
      "excludePackagePrefixes": ["@luxuryescapes/", "circleci/"]
    },
    {
      "groupName": "Node",
      "matchPackageNames": ["cimg/node", "node", "@types/node"]
      //only allow updates to even numbered versions eg 16.xx.xx
      "allowedVersions": "/^[1–2](0|2|4|6|8)\\.\\d+\\.\\d+$/"
    }
  ],
  "prConcurrentLimit": 5,
  //wait until CI has finished to raise PR (fail or pass)
  "prCreation": "not-pending",
  //if CI has not finished after 24 hours, raise PR anyway
  "prNotPendingHours": 24,
  //bump the range even if the new version satisfies the existing range, e.g. ^1.0.0 -> ^1.1.0
  "rangeStrategy": "bump",
  //PRs will be raised separately for each available major upgrade version.
  "separateMultipleMajor": true
}
```
