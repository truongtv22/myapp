## Motivation
Extending the react-native-config/fastlane template to cover react-native-version and OTA updates. Byebye to the days of 300+ lines of script to build ios/android with hard-coded in config. Bring some 12 factor love to your mobile apps!

## Development environment setup
Install Node(10.15)

`nvm install 10.15` or `brew install node`

Install watchman(4.9.0)

`brew install watchman`

Install yarn

`brew install yarn --ignore-dependencies`

Install CocoaPods: [React-Native CocoaPods](https://facebook.github.io/react-native/docs/integration-with-existing-apps#3-install-cocoapods)

`brew install cocoapods`

### iOS setup

Please refer to https://facebook.github.io/react-native/docs/getting-started

1. Install Xcode
2. Install Xcode Command Line tools `xcode-select --install`
3. Install node modules `yarn`
4. Install CocoaPods dependencies `cd ios && pod install`

## Typescript
This project is initiated with `npx --ignore-existing react-native init <project-name> --template react-native-template-typescript`

## Secrets & Environment Variables
This project uses [react-native-config](https://github.com/luggit/react-native-config) to expose config variables to your javascript code in React Native. The `.env` files are ignored by git keeping those secrets out of your repo.

#### Get started for local development:
1. Copy `.env.example` to `.env.local` or `.env`
2. Add your config variables
3. Follow instructions at [https://github.com/luggit/react-native-config#setup](https://github.com/luggit/react-native-config#setup)
4. Secrets are usually kept in `.env.secret` and should NEVER be git committed

## Fastlane
Please make sure you update `fastlane/Fastfile` with the correct config and syntax according to [Fastlane docs](https://docs.fastlane.tools/)

+ for iOS, please note if `XCODE_AUTO_CODE_SIGN` should be true or false (manually manage code-signing)

Fastlane will load config from `/config.*` file into `.env`
Secrets are to be provided in command line

+ `MYAPP_CONFIG=prod yarn fastlane:ios-ci`
+ `MYAPP_KEYSTORE_PASSWORD=xxxxx MYAPP_CONFIG=prod yarn fastlane:android-ci`

#### References:
+ [2018 React Native DevOps Guide](https://medium.com/@tgpski/react-native-devops-guide-2d8e4755ebee)
+ [2017 Fastlane Devops with RN](https://medium.com/react-native-training/fastlane-for-react-native-ios-android-app-devops-8ca85bee614e)

## Versioning ###
There should be 2 versioning: App(Container) version and Core version. 

For example, an app label 1.3.0(49)-v8. App version is 1.3.0; core version is v8; build number is 49.

#### App Versioning (for ipa/apk version)
Follow semantic versioning practice. Normally, you will only bump version after a sprint.
1. Manually update the version in `package.json`.
2. Bump App version: `yarn postversion:app -B`
3. Commit and push your code

Notes: 

You can also run `npm version <newversion>`. You will see the latest version updated in `package.json`. 

You can also bumping build number(not app version): `yarn postversion:app -b` 

#### Core Versioning (for js bundle)
To understand how Over-the-air(OTA) updates work, please refer to the [docs](https://microsoft.github.io/code-push/)

Follow code-push's practice by v1, v2 etc.
