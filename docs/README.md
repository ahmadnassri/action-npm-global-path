GitHub Actions doesn't play nicely with `npm install --global` without `sudo`, nor does it allow it to be easily cached.

This Action will change npm's behavior to:

- use `npm install --global` without `sudo`
- change the global install path to `<path>/packages`
- update the `$PATH` search path to include the new global npm install path for binary execution
- change the npm cache path to `<path>/cache`

## Usage

```yaml
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

      - uses: ahmadnassri/action-npm-global-path
        with:
          path: ~/.my-npm-stuff
```

### Inputs

| input | required | default  | description      |
| ----- | -------- | -------- | ---------------- |
| path  | ❌        | `~/.npm` | root path to use |
