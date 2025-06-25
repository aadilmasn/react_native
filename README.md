## Step 1: Create Project
```bash
npx @react-native-community/cli@latest init NameSomething
```
## Step 2: Dependencies
### Remove ESLint
```bash
npm uninstall jest react-test-renderer typescript eslint @react-native/eslint-config @react-native/new-app-screen @react-native/typescript-config @types/jest @types/react @types/react-test-renderer
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
npm install react-native-vector-icons
```
### Icons Setup
#### android/app/build.gradle
```bash
apply from: "../../node_modules/react-native-vector-icons/fonts.gradle" //starting
implementation project(':react-native-vector-icons') //inside dependencies
```
#### android/settings.gradle
```bash
include ':react-native-vector-icons'
project(':react-native-vector-icons').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-vector-icons/android')
```
#### android/app/src/main --> create folders --> /assets/fonts
```bash
mkdir assets
cd assets
mkdir fonts
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
## Step 3: Sample Folder Structure
<pre> <code> 
  src
  ├── assets
  │ └── logo.png 
  ├── components
  │ └── ProductCard.jsx 
  ├── config
  │ └── Socket.js 
  ├── customs
  │ └── ThemedView.jsx
  ├── hooks
  │ └── AddProduct.jsx 
  ├── layout
  │ └── Stack.jsx 
  ├── navigations
  │ └── BottomTab.jsx 
  ├── screens
  │ └── ProductScreen.jsx 
  ├── standards
  │ └── Colors.js 
  └── utils
    └── sampleData.js 
</code> </pre>
## Step 4: Create Folders
### Note: Use it in Git Bash
```bash
mkdir -p src/{components,screens,utils,standards,assets,navigations,layout,config,customs,helpers,hooks}
```
## Step 5: Redux Setup
### src/storage/redux/store.js
```bash
import { configureStore } from '@reduxjs/toolkit';
import { persistStore, persistReducer } from 'redux-persist';
import AsyncStorage from '@react-native-async-storage/async-storage';
import rootReducer from './root';

const persistConfig = {
    key: 'root',
    storage: AsyncStorage,
    whitelist: ['counter'],
};

const persistedReducer = persistReducer(persistConfig, rootReducer);

export const store = configureStore({
    reducer: persistedReducer,
    middleware: getDefaultMiddleware =>
        getDefaultMiddleware({
            serializableCheck: false,
        }),
});

export const persistor = persistStore(store);
```
### src/storage/redux/root.js
```bash
import { combineReducers } from '@reduxjs/toolkit';
import counterReducer from '../slice/counter';

const rootReducer = combineReducers({
  counter: counterReducer,
});

export default rootReducer;
```

### src/storage/slice/counter.js
```bash
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  value: 0,
};

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: state => {
      state.value += 1;
    },
    decrement: state => {
      state.value -= 1;
    },
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

### src/screens/Counter.jsx
```bash
import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import { useDispatch, useSelector } from 'react-redux';
import { increment, decrement } from './storage/slice/counter';

export default function Counter() {
  const dispatch = useDispatch();
  const count = useSelector(state => state.counter.value);

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Count: {count}</Text>
      <Button title="Increment" onPress={() => dispatch(increment())} />
      <Button title="Decrement" onPress={() => dispatch(decrement())} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', alignItems: 'center' },
  title: { fontSize: 24, marginBottom: 20 },
});

```

### App.jsx
```bash
import React from 'react';
import { Provider } from 'react-redux';
import { PersistGate } from 'redux-persist/integration/react';
import { store, persistor } from './src/storage/redux/store';
import { ActivityIndicator } from 'react-native';
import Counter from './src/Counter';

export default function App() {
  return (
    <Provider store={store}>
      <PersistGate loading={<ActivityIndicator />} persistor={persistor}>
        <Counter />
      </PersistGate>
    </Provider>
  );
}
```

## Step 6: Create Navigations

