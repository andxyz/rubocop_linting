# Reason

This app lets me test out different rubocop setups. 

Typically I try to make this codebase contain the lastest and greatest rubocop rules.

Sometimes you can get the application code to pass both checks.
- CI has it's version of rubocop.
- Now locally we can test the modified files with the latest rubocop setup available

## Usage

Test it out with:

```shell
bundle exec rubocop --config .rubocop.yml Gemfile
```

Called via something like: `git rubocop-against-master-latest-rubocop-linting-rules.sh`

Setup with something like:

```shell
$ cat `which git-rubocop-against-master-latest-rubocop-linting-rules.sh`
#!/usr/bin/env bash

rubo_files=$(git diff --diff-filter AM --name-only master | xargs -I{} ls $PWD/{} |
ggrep -Ei '.rb|.rake|.podspec|.jbuilder|Gemfile|Rakefile|Podfile|Thorfile|Fastfile|Vagrantfile')

echo ""
echo ""

cd "${HOME}"/code/rubocop_linting/

set -x
set -e

bundle exec rubocop --require rubocop-rspec --display-cop-names --config "${HOME}"/code/rubocop_linting/.rubocop.yml --force-exclusion ${rubo_files}
```
