## Step 1: Create Project
```bash
npx @react-native-community/cli@latest init NameSomething
```
## Step 2: Dependencies
### Remove ESLint
```bash
npm uninstall eslint @react-native/eslint-config
```
### Add State Management
```bash
npm install redux react-redux redux-persist @reduxjs/toolkit @react-native-async-storage/async-storage
```
### Add Navigations
```bash
npm install react-native-screens react-native-safe-area-context @react-navigation/native @react-navigation/native-stack @react-navigation/bottom-tabs @react-navigation/material-top-tabs 
```
### Add Tabs View
```bash
npm install react-native-tab-view react-native-pager-view 
```
### Add Icons
```bash
npm install react-native-vector-icon
```
### Add Animations
```bash
npm install react-native-reanimated react-native-gesture-handler
```
### Add Firebase
```bash
npm install firebase
```
### Add Payment Gateway
```bash
npm install react-native-razorpay
```
## Step 3: Folder Structure
<pre> <code> ```text my-project/ ├── assets/ │ └── logo.png ├── components/ │ ├── Header.js │ └── Footer.js ├── screens/ │ ├── HomeScreen.js │ └── DetailScreen.js ├── App.js └── package.json ``` </code> </pre>
```bash

```
