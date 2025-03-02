# XMLLint Validate

<div aria-hidden="true">

[![Latest Stable Version](https://img.shields.io/github/v/release/PHPCSStandards/xmllint-validate?label=Stable)](https://github.com/PHPCSStandards/xmllint-validate/releases)
[![Test](https://github.com/PHPCSStandards/xmllint-validate/actions/workflows/test.yml/badge.svg?branch=develop)](https://github.com/PHPCSStandards/xmllint-validate/actions/workflows/test.yml)
[![License](https://img.shields.io/github/license/PHPCSStandards/xmllint-validate)](https://github.com/PHPCSStandards/xmllint-validate/blob/develop/LICENSE)

</div>

GitHub Action to validate XML files for being well-formed and optionally validate against an XSD schema file.


## Action inputs

| Input        | Required | Type   | Notes                                                                                 |
|--------------|----------|--------|---------------------------------------------------------------------------------------|
| `pattern`    | yes      | string | The file(s) to validate. The input expects a path to a single file or a glob pattern. |
| `xsd-file`   | no       | string | Path to a local file containing the XSD schema to validate against.                   |
| `xsd-url`    | no       | string | URL to a remote file containing the XSD schema to validate against.                   |
| `show-in-pr` | no       | bool   | Annotate any errors from xmllint inline in PRs ? Defaults to `true`.                  |
| `debug`      | no       | bool   | Show verbose output to allow for debugging the action. Defaults to `false`.           |

> [!NOTE]
> If both an `xsd-file` and an `xsd-url` are passed, the `xsd-file` takes precedence.

## Using the action

Validating the well-formedness of a single XML file:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML file
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "path/to/file.xml"
```

Glob patterns are also supported:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML files
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "path/to/*/docs/*.xml"
```

Validating XML files against a locally available XSD schema:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML file
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "path/to/*/docs/*.xml"
          xsd-file: "path/to/docs.xsd"
```

Validating XML files against a remote XSD schema:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML file
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "path/to/*/docs/*.xml"
          xsd-url: "https://examples.org/docs.xsd"
```

## Example usage

Some examples of how this action can be used:

### Validate XSD files in a repo against the official specs

```yaml
jobs:
  test:
    name: "Validate XSD files"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XSD files conform to the specs
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "path/to/*.xsd"
          xsd-url: "https://www.w3.org/2012/04/XMLSchema.xsd"
```

### Validate a PHP_CodeSniffer XML configuration file against the XSD of the installed version

The below workflow presumes [PHP_CodeSniffer] will be installed via [Composer].

```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Install PHP
        uses: shivammathur/setup-php@v2

      - name: Install Composer dependencies
        uses: "ramsey/composer-install@v3"

      - name: Validate PHP_CodeSniffer XML ruleset
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "phpcs.xml.dist"
          xsd-file: "vendor/squizlabs/php_codesniffer/phpcs.xsd"
```

### Validate a PHPUnit XML configuration file against the XSD of the installed version

The below workflow presumes [PHPUnit] will be installed via [Composer].

```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Install PHP
        uses: shivammathur/setup-php@v2

      - name: Install Composer dependencies
        uses: "ramsey/composer-install@v3"

      - name: Validate PHPUnit XML configuration against current
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "phpunit.xml.dist"
          xsd-file: "vendor/phpunit/phpunit/phpunit.xsd"

      # Or alternatively:
      - name: Validate PHPUnit XML configuration against older XSD
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "phpunit.xml.dist"
          xsd-file: "vendor/phpunit/phpunit/schema/9.2.xsd"
```


## Contributing

Contributions to this project are welcome. Clone this repository, create a new branch, make your changes, commit them and send in a pull request.

If unsure whether the changes you are proposing would be welcome, open an issue first to discuss your proposal.


## Funding

This project is part of the [PHPCSStandards Open Collective](https://opencollective.com/php_codesniffer) and financial support for this project is always appreciated!


## Copyright and License

The phpcsstandards/xmllint-validate GitHub Action is [©copyright PHPCSStandards and contributors](https://github.com/PHPCSStandards/xmllint-validate/graphs/contributors) and licensed for use under the terms of the MIT License (MIT).
Please see [LICENSE](LICENSE) for more information.


### Other Credits

This action gratefully makes use of the following externally provided tools which are each governed by their own licensing:

* [`xmllint](https://gnome.pages.gitlab.gnome.org/libxml2/xmllint.html)
* [`xmllint-problem-matcher`](https://github.com/korelstar/xmllint-problem-matcher)
* [`wget`](https://www.gnu.org/software/wget/)


[Composer]:        https://getcomposer.org
[PHPUnit]:         https://phpunit.de/index.html
[PHP_CodeSniffer]: https://github.com/PHPCSStandards/PHP_CodeSniffer
