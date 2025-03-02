# openwrt-package-mirror-hash-calculator

A script to calculate the `PKG_MIRROR_HASH` value for OpenWrt packages.</br>
When executed, it changes the value of `PKG_MIRROR_HASH` in the Makefile and commit it.

## Usage

``` yaml
name: Openwrt Build Bot
on:
  workflow_dispatch:
    inputs:
      target_version:
        description: 'Target OpenWrt version. if empty the simple mode will be used.'
        required: false
        type: string
  workflow_call:
    inputs:
      target_version:
        required: false
        type: string
  push:
    branches:

jobs:
  check:
    name: Calculating PKG_MIRROR_HASH of XX
    runs-on: ubuntu-latest
    permissions:
      contents: write  # To push a branch

    steps:
      - uses: actions/checkout@v4
        with:
          ref: ${{ github.ref_name }}
          fetch-depth: 0

      - uses: muink/openwrt-package-mirror-hash-calculator@main
        env:
          COMMIT_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          MAKEFILE: Makefile
          TARGET_VERSION: ${{ inputs.target_version }}
```
