# changelogen

[![npm version][npm-version-src]][npm-version-href]
[![npm downloads][npm-downloads-src]][npm-downloads-href]
[![License][license-src]][license-href]

This is a fork version from [unjs/changelogen](https://github.com/unjs/changelogen). I made some modification to fit Github Action workflow.

## Changes

- Remove `--bump`, and updating `package.json`, which means you should tag your repo yourself and modify version in your package manager, such as `package.json`, `Cargo.toml`, etc.

## Examples
```yaml
name: Release Changelog

on:
  push:
    tags:
      - 'v*'

permissions:
  contents: write

jobs:
  changelog:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          ref: main

      - name: Setup git config
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "41898282+github-actions[bot]@users.noreply.github.com"

      - name: Release changelog
        run: npx changelogen-gh --release --push
        env:
          GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}
```
This will:
1. generate changelog from previous tag to current tag.
2. make a new commit and push to remote repo.
3. create/update release in Github release.

> [!WARNING]
> I haven't tested other functions, for details of my modification please check this [commit](https://github.com/uchouT/changelogen/commit/19a4a55e9b3d64eca57791822c74acd8c059d6a1).

[npm-version-src]: https://img.shields.io/npm/v/changelogen-gh?style=flat&colorA=18181B&colorB=F0DB4F
[npm-version-href]: https://npmjs.com/package/changelogen-gh
[npm-downloads-src]: https://img.shields.io/npm/dm/changelogen-gh?style=flat&colorA=18181B&colorB=F0DB4F
[npm-downloads-href]: https://npmjs.com/package/changelogen-gh
[license-src]: https://img.shields.io/github/license/uchouT/changelogen.svg?style=flat&colorA=18181B&colorB=F0DB4F
[license-href]: https://github.com/uchouT/changelogen/blob/main/LICENSE
