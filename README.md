check-manifest
--------------

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
| args                |  `string`   |    `false`    |  `''` | Arguments passed directly to [check-manifest](https://github.com/mgedmin/check-manifest#command-line-reference)            |
| version         |  `string`   |    `false`    | `0.46` | Version of  [check-manifest](https://github.com/mgedmin/check-manifest/tags)  |



## Example

- Update the `MANIFEST.in` using the suggesstions from [check-manifest](https://github.com/mgedmin/check-manifest)

```yaml
...
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Set up Python 3.6
        uses: actions/setup-python@v2
        with:
          python-version: '3.6'
      - uses: actions/cache@v2
        id: pip-cache
        with:
          path: ~/.cache/pip
          key: ${{ runner.os }}-pip-
          restore-keys: |
            ${{ runner.os }}-pip-
      - name: Run check-manifest
        uses: ./
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
          token: ${{ secrets.PAT_TOKEN }}

```


* Free software: [MIT license](LICENSE)

Features
--------

* Running [check-manifest](https://github.com/mgedmin/check-manifest) against a specified package.


Credits
-------

This package was created with [Cookiecutter](https://github.com/cookiecutter/cookiecutter).



Report Bugs
-----------

Report bugs at https://github.com/tj-actions/check-manifest/issues.

If you are reporting a bug, please include:

* Your operating system name and version.
* Any details about your workflow that might be helpful in troubleshooting.
* Detailed steps to reproduce the bug.
