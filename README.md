# timdev/devtools

## What's this?

A little package to try to standardize a set of development tools for PHP 
projects. Probably not of interest to anyone who isn't working on projects with
me.

Including this package as a dev-dependency gets you:

* [PHPUnit] for testing.
* [Psalm] for static analysis.
* [PHPStan] for another flavor of static analysis.
* [PHP_CodeSniffer] for linting
* [Roave Security Advisories] to help avoid depending on packages with 
  vulnerabilities.

Along with config files for each.

## Motivation

The key motivation is to be able to share configurations for things like psalm,
php_cs, and phpunit between my projects, and keep things largely in sync.

## Assumptions

This package assumes your code is in `src/` and your tests are in `tests/`. It
further assumes that you want psalm and phpcs to be run on your test sources.

## Usage

Set `minimum-stability`:

```sh
# Because this package includes roave/security-advisories which, by design,
# will never have a stable release:
composer config minimum-stability dev

# you'll almost certainly also want to do:
composer config prefer-stable true    
```

Add this package a dev-dependency:

```sh
composer install --dev timdev/devtools
```

Run the setup script which will copy the three config files into your
project root:

```sh
vendor/bin/devtools-setup
```

Psalm is configured to use a baseline file, and will complain if there isn't
one. If you project does not already have a `psalm-baseline.xml` file in its
root directory, `devtools-setup` will install an empty baseline file for you, so
that psalm will run without error.

### Local Tweaks

Do not make changes to any of the `.xml.dist` files installed by 
`devtools-setup`. Your changes will be overwritten during an upgrade. Instead,
you should add non-`.dist` versions.

## Upgrading

Since the main point of this package is to manage local configuration for 
various tools, you should re-run `vendor/bin/devtools-setup` after upgrading
this package.

## Inspiration

I created this package after experimenting with [ramsey/devtools], which is an
incredibly cool thing. But I wanted something more focused on our needs at 
TimDev Software.

[PHPUnit]: https://phpunit.de/
[Psalm]: https://psalm.dev/
[PHPStan]: https://phpstan.org/
[PHP_CodeSniffer]: https://github.com/squizlabs/PHP_CodeSniffer
[Roave Security Advisories]: https://github.com/roave/security-advisories
[ramsey/devtools]: https://github.com/ramsey/devtools
