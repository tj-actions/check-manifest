[![Codacy Badge](https://api.codacy.com/project/badge/Grade/8d94ad31570d41a7b37407e0c5453367)](https://app.codacy.com/gh/tj-actions/check-manifest?utm_source=github.com\&utm_medium=referral\&utm_content=tj-actions/check-manifest\&utm_campaign=Badge_Grade_Settings)
[![CI](https://github.com/tj-actions/check-manifest/actions/workflows/test.yml/badge.svg)](https://github.com/tj-actions/check-manifest/actions/workflows/test.yml)
[![Update release version.](https://github.com/tj-actions/check-manifest/actions/workflows/sync-release-version.yml/badge.svg)](https://github.com/tj-actions/check-manifest/actions/workflows/sync-release-version.yml)
[![Public workflows that use this action.](https://img.shields.io/endpoint?url=https%3A%2F%2Fused-by.vercel.app%2Fapi%2Fgithub-actions%2Fused-by%3Faction%3Dtj-actions%2Fcheck-manifest%26badge%3Dtrue)](https://github.com/search?o=desc\&q=tj-actions+check-manifest+path%3A.github%2Fworkflows+language%3AYAML\&s=\&type=Code)

## check-manifest

Run [check-manifest](https://github.com/mgedmin/check-manifest) to detect issues with distributed python packages.

```yaml
...
    steps:
      - uses: actions/checkout@v4
      - name: check-manifest
        uses: tj-actions/check-manifest@v1
```

## Inputs

<!-- AUTO-DOC-INPUT:START - Do not remove or modify this section -->

|                               INPUT                               |  TYPE  | REQUIRED | DEFAULT  |            DESCRIPTION             |
|-------------------------------------------------------------------|--------|----------|----------|------------------------------------|
|           <a name="input_args"></a>[args](#input_args)            | string |  false   |  `"-v"`  | Arguments passed to check-manifest |
| <a name="input_package-dir"></a>[package-dir](#input_package-dir) | string |  false   |          |      Directory of the package      |
|       <a name="input_version"></a>[version](#input_version)       | string |   true   | `"0.46"` |  Pinned version of check-manifest  |

<!-- AUTO-DOC-INPUT:END -->

## Example

*   Update the `MANIFEST.in` using the suggestions from [check-manifest](https://github.com/mgedmin/check-manifest)

```yaml
...
    steps:
      - name: Checkout
        uses: actions/checkout@v4
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
