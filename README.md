# npm Global Path

configure GitHub Actions to work with npm --global

[![license][license-img]][license-url]
[![release][release-img]][release-url]
[![super linter][super-linter-img]][super-linter-url]
[![semantic][semantic-img]][semantic-url]

GitHub Actions doesn't play nicely with `npm install --global` without `sudo`, nor does it allow it to be easily cached.

This Action will change npm's behavior to:

-   use `npm install --global` without `sudo`
-   change the global install path to `<path>/packages`
-   update the `$PATH` search path to include the new global npm install path for binary execution
-   change the npm cache path to `<path>/cache`

## Usage

``` yaml
on: push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/cache@v2.1.4
        with:
          key: ${{ hashFiles('**/package-lock.json') }}
          path: |
            ~/.my-npm-stuff
            node_modules

      - uses: ahmadnassri/action-npm-global-path@v1
        with:
          path: ~/.my-npm-stuff
```

### Inputs

| input | required | default  | description      |
|-------|----------|----------|------------------|
| path  | ❌        | `~/.npm` | root path to use |

----
> Author: [Ahmad Nassri](https://www.ahmadnassri.com/) &bull;
> Twitter: [@AhmadNassri](https://twitter.com/AhmadNassri)

[license-url]: LICENSE
[license-img]: https://badgen.net/github/license/ahmadnassri/action-npm-global-path

[release-url]: https://github.com/ahmadnassri/action-npm-global-path/releases
[release-img]: https://badgen.net/github/release/ahmadnassri/action-npm-global-path

[super-linter-url]: https://github.com/ahmadnassri/action-npm-global-path/actions?query=workflow%3Asuper-linter
[super-linter-img]: https://github.com/ahmadnassri/action-npm-global-path/workflows/super-linter/badge.svg

[semantic-url]: https://github.com/ahmadnassri/action-npm-global-path/actions?query=workflow%3Arelease
[semantic-img]: https://badgen.net/badge/📦/semantically%20released/blue
