[![CI](https://github.com/tj-actions/check-manifest/actions/workflows/test.yml/badge.svg)](https://github.com/tj-actions/check-manifest/actions/workflows/test.yml) [![Update release version.](https://github.com/tj-actions/check-manifest/actions/workflows/sync-release-version.yml/badge.svg)](https://github.com/tj-actions/check-manifest/actions/workflows/sync-release-version.yml) [![Public workflows that use this action.](https://img.shields.io/endpoint?url=https%3A%2F%2Fapi-tj-actions1.vercel.app%2Fapi%2Fgithub-actions%2Fused-by%3Faction%3Dtj-actions%2Fcheck-manifest%26badge%3Dtrue)](https://github.com/search?o=desc\&q=tj-actions+check-manifest+path%3A.github%2Fworkflows+language%3AYAML\&s=\&type=Code)

## check-manifest

Run [check-manifest](https://github.com/mgedmin/check-manifest) to detect issues with distributed python packages.

```yaml
...
    steps:
      - uses: actions/checkout@v2
      - name: check-manifest
        uses: tj-actions/check-manifest@v1
```

## Inputs

|   Input       |    type    |  required     |  default                      |  description  |
|:-------------:|:-----------:|:-------------:|:----------------------------:|:-------------:|
| package-dir         |  `string`   |    `false`    |  `''` | Directory of the package             |
| args                |  `string`   |    `false`    |  `-v` | Arguments passed directly to [check-manifest](https://github.com/mgedmin/check-manifest#command-line-reference)            |
| version         |  `string`   |    `true`    | `0.46` | Version of  [check-manifest](https://github.com/mgedmin/check-manifest/tags)  |

## Example

*   Update the `MANIFEST.in` using the suggestions from [check-manifest](https://github.com/mgedmin/check-manifest)

```yaml
...
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Set up Python 3
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'
      - uses: actions/cache@v2
        id: pip-cache
        with:
          path: ~/.cache/pip
          key: ${{ runner.os }}-pip-
          restore-keys: |
            ${{ runner.os }}-pip-
      - name: Run check-manifest
        uses: tj-actions/check-manifest@v1
        with:
          package-dir: 'test_package'
          args: '-u'
      - name: Create Pull Request
        if: failure()
        uses: peter-evans/create-pull-request@v3
        with:
          base: "main"
          title: "Updated MANIFEST.in"
          branch: "chore/update-manifest-in"
          commit-message: "Updated MANIFEST.in"
          body: "Updated MANIFEST.in"
          token: ${{ secrets.github_token }}

```

*   Free software: [MIT license](LICENSE)

If you feel generous and want to show some extra appreciation:

[![Buy me a coffee][buymeacoffee-shield]][buymeacoffee]

[buymeacoffee]: https://www.buymeacoffee.com/jackton1

[buymeacoffee-shield]: https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png

## Features

*   Running [check-manifest](https://github.com/mgedmin/check-manifest) against a specified package.

## Credits

This package was created with [Cookiecutter](https://github.com/cookiecutter/cookiecutter).

## Report Bugs

Report bugs at https://github.com/tj-actions/check-manifest/issues.

If you are reporting a bug, please include:

*   Your operating system name and version.
*   Any details about your workflow that might be helpful in troubleshooting.
*   Detailed steps to reproduce the bug.
