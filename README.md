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
