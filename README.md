A better pre-commit hook for git.

[![Current version](https://badge.fury.io/rb/pre-commit.png)](https://rubygems.org/gems/pre-commit)
[![Code Climate](https://codeclimate.com/github/jish/pre-commit.png)](https://codeclimate.com/github/jish/pre-commit)
[![Coverage Status](https://coveralls.io/repos/jish/pre-commit/badge.png?branch=master)](https://coveralls.io/r/jish/pre-commit?branch=master)
[![Build status](https://secure.travis-ci.org/jish/pre-commit.png?branch=master)](https://travis-ci.org/jish/pre-commit)
[![Dependency Status](https://gemnasium.com/jish/pre-commit.png)](https://gemnasium.com/jish/pre-commit)
[![Documentation](http://b.repl.ca/v1/yard-docs-blue.png)](http://rubydoc.info/gems/pre-commit/frames)

## Installation

Install the gem

    $ gem install pre-commit

Use the pre-commit command to generate a stub pre-commit hook

    # In your git repo
    $ pre-commit install

This creates a .git/hooks/pre-commit script which will check your git config and run checks that are enabled.

## Available checks

These are the available checks:

* white_space
* console_log
* debugger
* pry
* tabs
* jshint
* js_lint
* closure\_syntax\_check
* php (Runs php -l on all staged files)
* rspec_focus (Will check if you are about to check in a :focus in a spec file)
* ruby_symbol_hashrockets (1.9 syntax. BAD :foo => "bar". GOOD foo: "bar")
* local (executes `config/pre-commit.rb` with list of changed files)
* merge_conflict (Will check if you are about to check in a merge conflict)
* migrations (Will make sure you check in the proper files after creating a Rails migration)
* ci (Will run the `pre_commit:ci` rake task and pass or fail accordingly)
* rubocop (Check ruby code style using the rubocop gem. Rubocop must be installed)
* before_all (Check your RSpec tests for the use of `before(:all)`)
* coffeelint (Check your coffeescript files using the [coffeelint gem.](https://github.com/clutchski/coffeelint))
* go (Runs go fmt on a go source file and fail if formatting is incorrect, then runs go build and fails if can't compile)
* scss_lint (Check your SCSS files using the [scss-lint gem](https://github.com/causes/scss-lint))
* yaml (Check that your YAML is parsable)
* json (Checks if JSON is parsable)

## Default checks

Use `pre-commit list` to see the list of default and enabled checks and warnings.

## Enabling / Disabling Checks / Warnings

### Git configuration

    git config pre-commit.checks "whitespace, jshint, debugger"

To disable, simply leave one off the list

    git config pre-commit.checks "whitespace, jshint"

### CLI configuration

```ssh
pre-commit <enable|disable> <git|yaml> <checks|warnings> check1 [check2...]
```

The `git` provider can be used for local machine configuration, the `yaml` can be used for shared
project configuration.

Example move `jshint` from `checks` to `warnings` in `yaml` provider and save configuration to git:
```bash
pre-commit disable yaml checks   jshint
pre-commit enable  yaml warnings jshint
git add config/pre_commit.yml
git commit -m "pre-commit: move jshint from checks to warnings"
```

Example `config/pre_commit.yml`:
```yaml
---
:warnings_remove: []
:warnings_add:
- :jshint
- :tabs
```

## Running test manually

This functionality was added in version `0.17.0`

```bash
pre-commit run              # run on the files added to index not yet commited
pre-commit run all          # run on all files in current directory
pre-commit run <file-list>  # run on the list of files, patterns not supported
```

## Configuration providers

`pre-commit` comes with 4 configuration providers:

- `default` - basic settings, read only
- `git` - reads configuration from `git config pre-commit.*`, allow local update
- `yaml` - reads configuration from `/etc/pre_commit.yml`, `$HOME/.pre_commit.yml` and `config/pre_commit.yml`, allows `config/pre_commit.yml` updates
- `env` - reads configuration from environment variables

## [Contributing](CONTRIBUTING.md)
