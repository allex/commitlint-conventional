> Lint your conventional commits

# @tdio/commitlint-conventional

Shareable `commitlint` config enforcing [conventional commits](https://conventionalcommits.org/).
Use with [@commitlint/cli](https://npm.im/@commitlint/cli) and [@commitlint/prompt-cli](https://npm.im/@commitlint/prompt-cli).

## Getting started

```sh
yarn add -D @tdio/commitlint-conventional @commitlint/cli
echo "module.exports = {extends: ['@tdio/commitlint-conventional']};" > .commitlintrc.js
```

## Rules
### Problems

The following rules are considered problems for `@tdio/commitlint-conventional` and will yield a non-zero exit code when not met.

Consult [docs/rules](https://conventional-changelog.github.io/commitlint/#/reference-rules) for a list of available rules.


#### type-enum
* **condition**: `type` is found in value
* **rule**: `always`
* **value**

  ```js
  [
    'ci',
    'chore',
    'docs',
    'feat',
    'fix',
    'improvement',
    'perf',
    'refactor',
    'revert',
    'style',
    'test',
    'ui'
  ]
  ```

```sh
echo "foo: some message" # fails
echo "fix: some message" # passes
```
* ci: Changes to our CI configuration files and scripts (example scopes: Circle, BrowserStack, SauceLabs)
* chore: Updating grunt tasks etc; no production code change
* docs: Documentation only changes
* feat: A new feature
* fix: A bug fix
* improvement: An improvement to a current feature
* perf: A code change that improves performance
* refactor: A code change that neither fixes a bug nor adds a feature
* style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* test: Adding missing tests or correcting existing tests
* ui: Common ui adjustments (example: Button, Layout, etc,.)

#### type-case
* **description**: `type` is in case `value`
* **rule**: `always`
* **value**
  ```js
    'lowerCase'
  ```

```sh
echo "FIX: some message" # fails
echo "fix: some message" # passes
```

#### type-empty
* **condition**: `type` is empty
* **rule**: `never`

```sh
echo ": some message" # fails
echo "fix: some message" # passes
```

#### scope-case
* **condition**: `scope` is in case `value`
* **rule**: `always`
```js
  'lowerCase'
```

```sh
echo "fix(SCOPE): some message" # fails
echo "fix(scope): some message" # passes
```

#### subject-case
* **condition**: `subject` is in one of the cases `['sentence-case', 'start-case', 'pascal-case', 'upper-case']`
* **rule**: `never`

```sh
echo "fix(SCOPE): Some message" # fails
echo "fix(SCOPE): Some Message" # fails
echo "fix(SCOPE): SomeMessage" # fails
echo "fix(SCOPE): SOMEMESSAGE" # fails
echo "fix(scope): some message" # passes
echo "fix(scope): some Message" # passes
```

#### subject-empty
* **condition**: `subject` is empty
* **rule**: `never`

```sh
echo "fix:" # fails
echo "fix: some message" # passes
```

#### subject-full-stop
* **condition**: `subject` ends with `value`
* **rule**: `never`
* **value**
```js
  '.'
```

```sh
echo "fix: some message." # fails
echo "fix: some message" # passes
```


#### header-max-length
* **condition**: `header` has `value` or less characters
* **rule**: `always`
* **value**
```js
  72
```

```sh
echo "fix: some message that is way too long and breaks the line max-length by several characters" # fails
echo "fix: some message" # passes
```
