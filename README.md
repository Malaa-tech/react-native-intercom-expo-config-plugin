This repo is a continuation on the work of https://github.com/expo/config-plugins since it is not updated frequently 

# Expo Config Plugin `@intercom/intercom-react-native`

An unofficial [Expo config plugin](https://docs.expo.io/guides/config-plugins) for easily setting up [React Native Intercom](https://github.com/intercom/intercom-react-native) with expo dev clients

## Installation

### Prerequisites

#### Versions >= 1.10

- App project using Expo SDK 48.
- Installed `expo-cli@4.4.4` or later.
- Installed `@intercom/intercom-react-native@4.0.1`
- For Android it Intercom requires `compileSdkVersion` and `targetSdkVersion` to be set on 33 or higher. [expo-build-properties](https://docs.expo.dev/versions/latest/sdk/build-properties/) is used to set it 

#### Versions < 1.10

- App project using Expo SDK 45.
- Installed `expo-cli@4.4.4` or later.
- Installed `@intercom/intercom-react-native@4.0.1`
- For Android it Intercom requires `compileSdkVersion` and `targetSdkVersion` to be set on 33 or higher. [expo-build-properties](https://docs.expo.dev/versions/latest/sdk/build-properties/) is used to set it

#### Versions < 1.3

- App project using Expo SDK 44.
- Installed `expo-cli@4.4.4` or later.
- Installed `@intercom/intercom-react-native`

#### With `expo install`

```
expo install react-native-intercom-expo-config-plugin expo-build-properties
```

#### Without `expo install`

```sh
# using yarn
yarn add react-native-intercom-expo-config-plugin expo-build-properties

# using npm
npm install react-native-intercom-expo-config-plugin expo-build-properties
```

Open your `app.json` and update your `plugins` section:

```json
{
  "plugins": [
    [
      "expo-build-properties",
      { "android": { "compileSdkVersion": 33, "targetSdkVersion": 33 } }
    ],
    "react-native-intercom-expo-config-plugin"
  ]
}
```

## Configuration

The plugin needs your intercom api key so that it can communicate with the intercom application.

```json
{
  "plugins": [
    [
      "creact-native-intercom-expo-config-plugin",
      {
        "iosApiKey": "<your-api-key>",
        "androidApiKey": "<your-api-key>",
        "appId": "<your-app-id>"
      }
    ]
  ]
}
```

### Other configuration options

<details>
<summary>Add a custom photo usage description</summary>

```json
{
  "plugins": [
    [
      "react-native-intercom-expo-config-plugin",
      {
        //...
        "iosPhotoUsageDescription": "Upload to support center"
      }
    ]
  ]
}
```

</details>

<details>
<summary>Add EU Region support</summary>

### On iOS Add to `app.json`

```json
{
  "ios": {
    "infoPlist:":{
        "IntercomRegion": "EU"
      }
  }
}

```

### On Android
```json
{
  "plugins": [
    [
      "react-native-intercom-expo-config-plugin",
      {
        //...
        "intercomEURegion": "true"
      }
    ]
  ]
}
```

</details>

<details>
<summary>Enable push notifications</summary>

### On iOS

```json
{
  "plugins": [
    [
      "react-native-intercom-expo-config-plugin",
      {
        //...
        "isPushNotificationsEnabledIOS": true
      }
    ]
  ]
}
```
### On Android

```json
{
  "plugins": [
    [
      "react-native-intercom-expo-config-plugin",
      {
        //...
        "isPushNotificationsEnabledAndroid": true,
        "androidIcon": "<string>" //Customize the icon for intercom push notifications from the intercom default
      }
    ]
  ]
}
```
</details>

## Android push notifications
If you want push notifications to fire when new messages are sent in a conversation, it is necesssary
to create a push notification channel for these. Push notifications for new conversations require no additoonal setup.
```jsx
useEffect(() => {
  if (Platform.OS === 'android') {
    Notifications.setNotificationChannelAsync('intercom_chat_replies_channel', {
      name: 'Intercom Replies Channel',
      description: 'Channel for intercom replies',
      importance: Notifications.AndroidImportance.MAX,
    })
  }
}, [])
```


## Building and running

You can either:

- use `expo prebuild` or `expo run:android`/`expo run:ios` to update your native projects,
- use _[EAS Build](https://docs.expo.io/build/introduction/)_ to build your development client.
  - Keep in mind that if you are using environment variables for `androidApiKey`, `iosApiKey` and `appId` in your `app.config.js`, you need to configure these secrets with `eas secret:create` or at _[Expo](https://expo.dev)_.

## Contributing

Contributions are very welcome! The package uses `expo-module-scripts` for most tasks. You can find detailed information [at this link](https://github.com/expo/expo/tree/master/packages/expo-module-scripts#-config-plugin).

Please make sure to run `yarn build`/`yarn rebuild` to update the `build` directory before pushing. The CI will fail otherwise.

## Credits

- _the Expo team_

- <https://github.com/expo/config-plugins>

## License

MIT
