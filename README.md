# PHP Codesniffer Rulesets + Sniffs

Using CIG PHP coding standards ruleset for PHP*CodeSniffer, you can analyse the
codebase of your project for PHP compatibility with other \_itcig* projects.

## What's in this repo ?

A ruleset for PHP*CodeSniffer to check for PHP compatibility and standards
across all \_itcig* PHP projects.

This WordPress specific ruleset prevents false positives from the
[PHPCompatibility standard](https://github.com/PHPCompatibility/PHPCompatibility)
by excluding back-fills and poly-fills which are provided by WordPress.

## Requirements

> These will all be installed automatically by this ruleset so you do not need
> to include them explicitly.

- [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer). Use the
  latest stable release of
  [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) for the best
  results. The minimum _recommended_ version of PHP_CodeSniffer is version
  3.0.2.
- [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility)
  9.0.0+.

## Installation instructions

The only supported installation method is via
[Composer](https://getcomposer.org/).

If you already have a Composer PHP_CodeSniffer plugin installed, run:

```bash
composer require --dev itcig/php-coding-standards:"*"
composer install
```

Next, run:

```bash
vendor/bin/phpcs -i
```

If all went well, you will now see that the `CIG`, `CIG-Docs`, `CIG-Wordpress`,
`CIG-Core`, `PHPCompatibility`, `PHPCompatibilityWP` and some more
PHPCompatibility standards are installed for PHP_CodeSniffer.

## How to use

Now you can use the following command to inspect your code:

```bash
./vendor/bin/phpcs -p . --standard=CIG
```

By default, you will only receive notifications about formatting and deprecated
and/or removed PHP features.

To get the most out of the CIG coding and PHPCompatibility standards, you should
specify a `testVersion` to check against. That will enable the checks for both
deprecated/removed PHP features as well as the detection of code using new PHP
features.

If you want to enforce the minimum PHP requirement, either add
`--runtime-set testVersion 7.2-` to your command-line command or add
`<config name="testVersion" value="7.2-"/>` to your
[custom ruleset](https://github.com/PHPCompatibility/PHPCompatibility#using-a-custom-ruleset).

For example:

```bash
# For a project which should be compatible with PHP 7.2 and higher:
./vendor/bin/phpcs -p . --standard=CIG --runtime-set testVersion 7.2-
```

For more detailed information about setting the `testVersion`, see the README of
the generic
[PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility#sniffing-your-code-for-compatibility-with-specific-php-versions)
standard.

### Testing PHP files only

By default PHP_CodeSniffer will analyse PHP, JavaScript and CSS files. As the
PHPCompatibility sniffs only target PHP code, you can make the run slightly
faster by telling PHP_CodeSniffer to only check PHP files, like so:

```bash
./vendor/bin/phpcs -p . --standard=CIG --extensions=php --runtime-set testVersion 7.2-
```
