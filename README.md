## React-Native-Ble-Manager-Wrapper

#### Continue to study and ponder to improve the code structure.

This is a wrapper module that provides the desired function through the use case and repository pattern divided by function without directly using react-native-ble-manager in the UI layer.

- Language: Typescript
- Structure Summary
  - ✨ assets
  - ✨ configs
  - ✨ data
  - ✨ domain
  - ✨ presentation
  - ✨ test
  - ✨ utils

#### Release Note

- 2023/03/03: Initialized react-native-ble-manager-wrapper project source code.
- 2023/03/04: Added utility sources (BLE, Alert, Common, Logger, Permission, Storage, Theme and Toast) - Not completed yet, Under construction.
- 2023/03/07: Deleted previous project source code.
- 2023/03/07: Created react-native typescript project again.

#### How To Setup Environment

It's mandantory to set up the development environment and build the app by following the instructions below:

- Visit https://reactnative.dev/docs/environment-setup
- Install Node, Brew, Yarn, Npm etc packages
- npx react-native init PROJECT_NAME --template react-native-template-typescript
- Set-up Android SDK path
- pod install
- Open iOS app project with Xcode IDE
- Set-up Bundle Identifier & Team account
- Build Clean + Re-build
- Set-up iOS device name in package.json
- rm -rf /Users/admin/Library/Developer/Xcode/DerivedData
- rm -rf Podfile.lock
- pod cache clean -all
- pod deintegrate
- pod install
- Clean & Re-build ios project
- Set-up Team account about Cocoapods AccessibilityReources
- When this error occurs, (Failed to build iOS project. We ran "xcodebuild" command.. ?)
  - Execute command, rm -rf /Users/admin/Library/Developer/Xcode/DerivedData
  - Execute Xcode
  - Check if DerivedData directory is made again.
  - Execute command, npm run ios again.
- When this error happens in Xcode, (error build: Command PhaseScriptExecution failed with a nonzero exit code)
  - sudo ln -s "$(which node)" /usr/local/bin/node
  - CMD + K: Clean Build
  - CMD + Shift + B : Build
  - npm run ios
  - Change package.json's ios setting: // "ios": "react-native run-ios", ==> "ios": "react-native run-ios --device='AidenKooG'",
  - Please check if mobile phone's developer mode is turned on.
- If encountering this error, cannot find ruby 2.7.6.. when you create new project ?
  - rbenv install 2.7.6
  - npx react-native init PROJECT_NAME --template react-native-template-typescript

#### BLE Configuration

Define the BLE uuid and other values you want in the BleConfig.js file below.

```sh
export const SERVICE_UUID = ''

export const RX_CHARACTERISTIC_UUID = ''
export const TX_CHARACTERISTIC_UUID = ''
export const FLOW_CONTROL_CHARACTERISTIC_UUID = ''

export const BATTERY_SERVICE_UUID = ''
export const BATTERY_CHARACTERISTIC_UUID = ''

export const BLE_TEST_MODE = false
export const BLE_TEST_DEVICE_NAME = ""
export const BLE_TEST_DEVICE_MAC_ADDRESS = ""

export const BLE_PROTOCOL_VERSION_INDEX = 0

export const BLE_PAIRING_VERSION = 0
export const BLE_PAIRING_RESULT_INDEX = 0
export const BLE_PAIRING_RESULT_SUCCESS = 0

export const BLE_NOTIFICATION_SUFFIX = 0
export const BLE_STATUS_INFO_SUFFIX = 0
```

#### Source Code

From UI To Core Module.

UI JSX Element.

```sh
return (
    <BluetoothComponent
        bleConnectionState={bleConnectionState}
        bleConnectionCompleteState={bleConnectionCompleteState}
    />
)
```

UseCase.

```sh
executeStartScanUseCase().catch((e) => {
    outputErrorLog(LOG_TAG, e + " occurred by executeStartScanUseCase")
})
```

Repository.

```sh
 const {
    connectDevice, disableNotification, disconnectDevice, enableNotification,
    initializeBleModule, getUuidList, sendBleCustomData, startScan, stopScan,
    getBleDeviceInfo
 } = BleRepository()

 executeStartScanUseCase = (serviceUuid = SERVICE_UUID, duration = SCAN_DURATION) => {
    return new Promise((fulfill, reject) => {
        startScan(serviceUuid, duration).then(() => {
            fulfill()
        }).catch((e) => {
            reject(e)
        })
    })
}

this.enableBluetooth().then(() => {
    bleManager.scan(serviceUuids, duration, false).then(() => {
        fulfill()
    }).catch((e) => {
        reject(e)
    })
}).catch((e) => {
    reject(e)
})
```

State Management.

```sh
const setBleScanningStateAtom = useSetRecoilState(bleScanningStateAtom)
const bleScanningState = useRecoilValue(bleScanningStateAtom)
```

#### Link

If you are interested in information about me or other activities, please access the link below.

| Plugin      | LINK                           |
| ----------- | ------------------------------ |
| Github page | [https://aidenkoog.github.io/] |
