# Build/Install

## Dependencies

* yarn \(npm fallback\)
* gulp-cli

### Installing dependencies

_npm is still possible to use, but yarn is much faster _[https://yarnpkg.com/](https://yarnpkg.com/)

Install yarn package-manager:

```
Choose your OS and install yarn https://yarnpkg.com/en/docs/install
```

Execute these commands on your server as a normal user to prepare the dependencies:

```bash
git clone https://github.com/ffrgb/meshviewer.git
cd meshviewer
yarn
# Only needed if no global gulp is installed / OS like arch provides a package
yarn global add gulp-cli
```

## Adjust config and style

1. [Change configuration to your community](/config_json.md)
2. \(optional\) Edit files in `scss/custom/`. Additional information in file comments and under [development](/development.md).
3. \(optional\) Change logo svg and generate new icons or adjaust the images yourself.

## Building

Just run the following command from the meshviewer directory:

```bash
gulp
```

This will generate the folder `build/` that will contain all required files.

