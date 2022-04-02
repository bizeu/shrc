# shrc 
![shrc](./.idea/icon.svg)
[![Build Status](https://github.com/j5pu/shrc/workflows/main/badge.svg)](https://github.com/j5pu/shrc/actions/workflows/main.yaml)

macOS and Linux Environment

## action
Multi Language Releaser Action and Scripts

## Examples:
```yaml
name: main

on:
  push:
  release:
  workflow_dispatch:

env:
  GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}

jobs:
  tests:
    runs-on: ${{ matrix.os }}
    strategy:
      fail-fast: true
      matrix:
        os: [ macos-latest, macos-10.15, ubuntu-latest, ubuntu-18.04 ]
    steps:
      - uses: actions/checkout@v3
      - uses: Homebrew/actions/setup-homebrew@master
        if: runner.os == 'macOS'
      - run: ./tests

  release:
    needs: [ tests ]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@main
        with:
          fetch-depth: 0
          token: "${{ env.GITHUB_TOKEN }}"
      - id: release
        uses: j5pu/shrc@main
```
