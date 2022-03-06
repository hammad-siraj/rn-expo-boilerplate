## Getting Started

In order to change app's name, please make necessary changes in `app.json`.

<details>
<summary>Manual setup</summary>

1. Clone the repo

```bash
> git clone App && cd App
```

3. Install packages

```bash
> yarn
```

4. Run it!

```bash
> yarn start
```

5. if you want to change the repo then run this command for pre-commit hooks

```bash
> npx husky install
```

</details>

## What's inside

- [Expo SDK](https://github.com/expo/expo) - a set of tools and services built around React Native and native platforms.
- [React Navigation (v6)](https://github.com/react-navigation/react-navigation) - routing and navigation for React Native apps.
- [RN UI lib](https://github.com/wix/react-native-ui-lib) - amazing Design System, UI toolset & components library for React Native. Dark Mode is implemented using this library.
- [Reanimated 2](https://github.com/software-mansion/react-native-reanimated) - React Native's Animated library reimplemented.
- [MobX](https://github.com/mobxjs/mobx) - simple, scalable state management, with [mobx-persist-store](https://github.com/quarrant/mobx-persist-store) for persisting your stores.
- ~~AsyncStorage~~ [MMKV](https://github.com/mrousavy/react-native-mmkv) - efficient, small mobile key-value storage framework developed by WeChat. [~30x faster](https://github.com/mrousavy/react-native-mmkv#benchmark) than _AsyncStorage_! Available only within Expo dev clients. Instructions on installation could be found [here](#ready-to-use-expo-config-plugins).

#### Extra helpful libraries

- [React Native Gesture Handler](https://github.com/kmagiera/react-native-gesture-handler) - native touches and gesture system for React Native.
- [ESLint](https://github.com/eslint/eslint) + [Prettier](https://github.com/prettier/prettier) - keep your code neat and structured.
- [Release It](https://github.com/release-it/release-it) - automate versioning and publishing of your app.
- [Typescript](https://www.typescriptlang.org/) - strict syntactical superset of JavaScript.

#### Useful services/methods

- `navigation` - a service where all navigation configuration takes place in. It simplifies and abstracts the process of registering screens, layouts, etc.
- `translate` - a service that brings easy integration of localization for an app by using [i18n-js](https://github.com/fnando/i18n-js) and [react-native-localize](https://github.com/zoontek/react-native-localize). You can see an example of `en` and `ru` localizations in `Example` screen.
- `onStart` - a service where you can write your own logic when app is launched. For example, you can increment number of `appLaunches` there.
- `configureDesignSystem()` - a method where all settings for an app's design system is taking place. You can customize there colors, schemes, typegraphy, spacings, etc.

https://user-images.githubusercontent.com/4402166/135329411-adb90a0a-c884-4bbb-9f62-33e9adbd3123.MP4

## Advantages

#### Ready-to-use Expo Config Plugins

It gives us ability to build custom dev clients for iOS and Android with pre-installed [react-native-mmvk](https://github.com/mrousavy/react-native-mmkv) and other libraries.

You can find available plugins under `./plugins` folders.

Links to the docs: [Expo Dev Clients](https://docs.expo.dev/clients/getting-started/) and [Expo Config Plugins](https://docs.expo.dev/guides/config-plugins).

<details>
<summary>Instructions for react-native-mmkv</summary>

1. Install [react-native-mmkv](https://github.com/mrousavy/react-native-mmkv) (compatible version - 1.3.2):

```bash
> yarn add react-native-mmkv@1.3.2
```

2. Open `app.json` and add the following:

```
{
  "expo": {
    ...
    "plugins": ["./plugins/withMMKV"],
    ...
  }
}
```

3. Start Expo dev server with for dev client

```bash
> expo start --dev-client
```

4. Run on a simulator or device

```bash
> expo run:ios # add -d to run on device
> expo run:android
```

5. Open `src/stores/_hydration.ts`, uncomment MMKV initialization code and enjoy its perfomance within Expo!

</details>

#### Describe app screens in one place

All setup for your screens takes place in one file `src/screens/index.ts`:

```
type Screen = 'Main' | 'Example' | 'Settings';
type Tabs = 'Main' | 'WIP' | 'Settings';

const screens: ScreenLayouts = {
  Main: {
    name: 'Main',
    component: Main,
    options: () => ({
      title: 'Home',
    }),
  },
  // ...
}

const tabs: TabScreenLayouts = {
  Main: {
    name: 'MainNavigator',
    component: HomeStack,
    options: () => ({
      title: 'Home',
    }),
  },
  // ...
}
```

#### Build layouts with ease

Stack Navigator:

```
const HomeStack = () =>
  genStackNavigator([
    screens.Main,
    screens.Example,
  ]);
```

Tab Navigator:

```
const TabNavigator = () =>
  genTabNavigator([
    tabs.Main,
    tabs.WIP,
    tabs.Settings,
  ]);
```

#### Navigate to other screens with predictability

```
const Screen = ({componentId}) => {
  const {nav} = useServices();

  return (
    <View>
      <Button
        onPress={() => nav.push('Settings')}
      />
    </View>
  )
}
```

1. Install this extension to get runtime eslint error : https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint

#### Samples for new screens, services, stores and components.

So you have one structure within the project. You can find them in corresponding folders. Just copy&paste it and make the necessary changes.

#### General

- [x] Passing props to a screen example
- [x] Constants: add Dimensions
- [x] AsyncStorage stores persisting example
- [x] Expo Web support
- [ ] Shared transitions — [IjzerenHein/react-navigation-shared-element](https://github.com/IjzerenHein/react-navigation-shared-element)

### CREDITS

THIS EXPO STARTER EXTENDS THE https://github.com/kanzitelli/expo-starter.git with some mine personal customizations.
