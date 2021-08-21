# timdev/devtools

## What's this?

A little package to try to standardize a set of development tools for PHP 
projects. Probably not of interest to anyone who isn't working on projects with
me.

Including this package as a dev-dependency gets you:

* PHPUnit for testing.
* Psalm for static analysis.
* PHP_CodeSniffer

Along with config files for each.

## Motivation

The key motivation is to be able to share configurations for things like psalm,
php_cs, and phpunit between my projects, and keep things largely in sync.

## Assumptions

This package assumes your code is in `src/` and your tests are in `tests/`. It
further assumes that you want psalm and phpcs to be run on your test sources.

## Usage

Add this package a dev-dependency:

```
composer install --dev timdev/devtools
```

Then run the setup script which will hard-link the three config files into your
project root:

```
vendor/bin/devtools-setup
```

Psalm is set up to use a baseline file, and will complain if there isn't one.
If you project does not already have a `psalm-baseline.xml` file in its root
directory, `devtools-setup` will install an empty baseline file for you, so that
psalm will run without error.

```
vendor/bin/psalm --set-baseline=psalm-baseline.xml
```

## Inspiration

I created this package after experimenting with [ramsey/devtools], which is an
incredibly cool thing. But I wanted something more minimal and malleable.


[ramsey/devtools]: https://github.com/ramsey/devtools
