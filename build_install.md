# Build/Install

## Dependencies

- yarn (npm fallback)
- grunt-cli

### Installing dependencies

_npm is still possible to use, but yarn is much faster https://yarnpkg.com/_

Install yarn package-manager:

    Choose your OS and install yarn https://yarnpkg.com/en/docs/install

Execute these commands on your server as a normal user to prepare the dependencies:

```bash
git clone https://github.com/ffrgb/meshviewer.git
cd meshviewer
yarn
# Only needed if no global grunt is installed
yarn global add grunt-cli
```

## Adjsut config and style

1. [Change configuration to your community](/config_json.md)

## Building

Just run the following command from the meshviewer directory:

```bash
grunt
```

This will generate the folder `build/` that will contain all required files.