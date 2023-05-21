# React-Native-Cheat-Sheet

Approaches
1. React Native CLI
2. Expo CLI

## With Expo CLI

# Setting Up Environment
1. Open Command Prompt 
 ``` 
 npm i -g expo-cli
 expo init ProjrectName
 ```
 
 2. Choose blank under Managed workflow
 
 3. Starting the project
  ``` 
 cd ProjrectName
 npm start
 ```
## Boilerplate
ProjectFile > App.js
```js
import { StatusBar } from  'expo-status-bar';

import { StyleSheet, Text, View } from  'react-native';

  

export  default  function  App() {

return (

<View  style={styles.container}>

<Text>Open up App.js to start working on your app!</Text>

<StatusBar  style="auto"  />

</View>

);

}

  

const  styles = StyleSheet.create({

container: {

flex: 1,

backgroundColor: '#fff',

alignItems: 'center',

justifyContent: 'center',

},

});
```
## Running The Application
1. In CMD
 ```
 npm start
 ```
 2. Go to: http://localhost:19000/ 
 3. Install "Expo Clint" App on mobile device
 4. Scan QR from device (both devices connected to same network)
 5. Shake mobile device to open developers menu
