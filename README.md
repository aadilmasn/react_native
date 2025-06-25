# React Native Setup
## Step 1: Create React Native Project
```bash
npx @react-native-community/cli@latest init NameSomething
```
## Step 2: Uninstall Dependencies
```bash
npm uninstall eslint @react-native/eslint-config
```
## Step 3: Install Dependencies
### a) State Management and Navigations
```bash
npm install @reduxjs/toolkit react-redux redux-persist @react-native-async-storage/async-storage @react-navigation/native @react-navigation/native-stack react-native-screens react-native-safe-area-context
```
### b) Icons and Animations
```bash
npm install react-native-vector-icon react-native-reanimated
```
