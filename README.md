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
| args                |  `string`   |    `false`    |  `''` | Arguments to pass directly to [check-manifest](https://github.com/mgedmin/check-manifest#command-line-reference)            |
| version         |  `string`   |    `false`    | `0.46` | Version of  [check-manifest](https://github.com/mgedmin/check-manifest/tags)  |


* Free software: [MIT license](LICENSE)

Features
--------

* TODO


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
