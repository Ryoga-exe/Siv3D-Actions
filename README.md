# Siv3D-Actions

[![Test-Windows](https://github.com/Ryoga-exe/Siv3D-Actions/actions/workflows/test-windows.yml/badge.svg)](https://github.com/Ryoga-exe/Siv3D-Actions/actions/workflows/test-windows.yml)
[![Test-Linux](https://github.com/Ryoga-exe/Siv3D-Actions/actions/workflows/test-linux.yml/badge.svg)](https://github.com/Ryoga-exe/Siv3D-Actions/actions/workflows/test-linux.yml)

GitHub Actions for [Siv3D](https://siv3d.github.io/) ♋ Setup Siv3D and build your apps.

Currently, supports Windows and Linux builds.

## Usage

### Example workflow

```yml
name: Test-Windows

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
  workflow_dispatch:

env:
  SOLUTION_FILE_PATH: "."
  SIV3D_VERSION: "0.6.13"
  APP_PATH: "./App"

permissions:
  contents: read

jobs:
  build:
    runs-on: windows-latest

    steps:
    - uses: actions/checkout@v3

    - name: Setup Siv3D and build
      uses: Ryoga-exe/Siv3D-Actions@latest
      with:
        siv3d-version: ${{ env.SIV3D_VERSION }}
        solution-path: ${{ env.SOLUTION_FILE_PATH }}

    - name: Publish App
      uses: actions/upload-artifact@v3
      with:
        name: App
        path: |
          ${{ env.APP_PATH }}
          !${{ env.APP_PATH }}/engine
          !${{ env.APP_PATH }}/AS_DEBUG
          !${{ env.APP_PATH }}/Screenshot
          !${{ env.APP_PATH }}/*.ico
          !${{ env.APP_PATH }}/Resource.rc
```
