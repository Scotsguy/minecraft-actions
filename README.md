# minecraft-actions
A repository of Minecraft Modding GitHub Actions for CI/CD

### Getting Started

To get started, create a file called `main.yml` in `./github/workflows`!

In `main.yml` paste this simple script!

```yaml
name: Build Mod
on: [push, pull_request]
jobs:
  gradle:
    strategy:
      matrix:
        os: [ubuntu-latest]
        java-version:
          - 8
    runs-on: ${{ matrix.os }}
    steps:
      - name: Checkout Project
        uses: actions/checkout@v1
        with:
          lfs: true

      - name: Setup Java
        uses: actions/setup-java@v1
        with:
          java-version: ${{ matrix.java-version }}

      - name: Allow Access
        run: chmod +x gradlew

      - name: Build Mod
        run: ./gradlew build --refresh-dependencies

      - name: Upload Artifact
        uses: actions/upload-artifact@v1
        with:
          name: Mod Builds
          path: build/libs
```

Advanced stuff coming soon! This repository is a working example.

This may work for forge but I don't care about forge so :).