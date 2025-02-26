# hlint-setup

GitHub Action: Set up hlint

Downloads a binary of HLint from [@ndmitchell/hlint](https://github.com/ndmitchell/hlint).

The which gets cached through [@actions/tool-cache](https://github.com/actions/tool-cache)

And adds it into `PATH`.

See also [haskell/actions/hlint-run](https://github.com/haskell/actions/hlint-run), which will run `hlint` and represent its output in GitHub annotations.

## Inputs

* `version`: The HLint version to download. Currently defaults to `3.1.6`.

## Outputs

* `hlint-dir`: Resulting directory containing the `hlint` executable
* `hlint-bin`: Location of the `hlint` executable
* `version`: Version of the `hlint` tool (same as input, if provided)

## Example

```yaml
name: lint
on:
  pull_request:
  push:
    branches:
      - master
      - 'releases/*'

jobs:
  hlint:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    - name: 'Set up HLint'
      uses: haskell/actions/hlint-setup@v1
      with:
        version: '3.1.6'

    - name: 'Run HLint'
      uses: haskell/actions/hlint-run@v1
      with:
        path: src/
        fail-on: warning
```
