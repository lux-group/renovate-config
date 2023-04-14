# renovate-config

This is the repo for our `default` implementation of renovate.json.

If most/all repo's extend this, then things like the npmtoken (necessary for updating some @luxuryescapes npm dependencies) can be
updated here and have that propagate to most repos.

# Config
```json
{
  "dependencyDashboard": true,
  "encrypted": {
    "npmToken": "wcFMA/xDdHCJBTolAQ//am1cZS5HMYp68HS4s7RXqQAMszPMpbDBcyZwxJ/lKl7BR8DhpxegbeaHVQLwdRlAEABCzbxoi/w3mpVlByr2Crok5SDYuoEOXigwlvFKXX3dnTpteULezLAxOzncuNW4CQlOrnTC5HiSvTjkfM9oqYnYdRRRVPYBBnOQKoQy60jHeDiFr4sV+jDup4MwuRjb04AJbGZcgGTo2U9FP8WcZSbh0BuI4gmMPwmOIIAK8RIEUEigpP7Tm9EqQzOv9rRl7nws1/HYhcmNX7EQey13tzc5q3vn6Odx4nWsOmdCV4qph1edURrbhYn0L+DGd7J+xu8yj7hUwdb22pBr76y2RXlF8Sywkmh035X6/Eof/nnKEnqzT0HPGVEqP9UeyvAoVedQ94j3FklQ1+CNjn74gTHT7cvmNXyxXGO4L5sqay2Ftt8USYpuJYr+AQhH6MnpVUXHHv2Zwoi29FVF68uNpIh/E7vY3Pi99dgwYa0GZM+8fR8mvZQ3DaxIWUAITcbGMzR0zvkNkjfcZWzuuTONy2yMwohMk9mpjRKmPZaegya8ErqHqyFb+S+Sbi/n0ImwedUco4W4P+pWF5g7110zmFEPu3u908pRs1Wz4oTpo0FzqLKa9m75BPSWuuxHw45UPGU8TG+CzNKbSfuiMJ+QS2t/omye4hB7SJ99bh82s+7SeAGVBGXK163bKgY8xzDP3z5bA1NyFZegAv568oT0QrCY93izezkffpA33kpuBK4bRYKCQuDMYq/pSZlxmmb+7BpkeyXh0jAtPlA3unX59ZV8EYu20JQEh6zXP58zK6aYwFcRtoJYwlZV+q4x52svdp7Nt3HHnM/1PA"
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
  "rangeStrategy": "replace",
  "separateMultipleMajor": true
}
```
