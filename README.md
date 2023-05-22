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

## Core Components and APIs
Refer to all components at: https://reactnative.dev/docs/components-and-apis
### View
`View` is designed to be nested inside other views and can have 0 to many children of any type.
```js
export  default  function  App() {
return (
	<View  style={styles.container}>
		<Text>Hello World !</Text>
	</View>
	);
}
```
**SafeAreaView**
- To take care of notch on phone
- `SafeAreaView` renders nested content and automatically applies padding to reflect the portion of the view that is not covered by navigation bars, tab bars, toolbars, and other ancestor views.
```js
export  default  function  App() {
return (
	<SafeAreaView  style={styles.container}>
		<Text>Hello World !</Text>
	</SafeAreaView>
	);
}
```

### Text
```js
const handlePress = () => console,log("Text Pressed");

<View style={styles.continer}>
	<Text numberOfLines={1}
		onPress={handlePress}>
		Hello World!
	</Text>
</View>

```
### Images
```js
<View style={styles.continer}>
	<Text>
		Hello World!
	</Text>
	<Image source={require('./assets/icon.png')} />
	<Image source={{ 
		width:200, 
		height: 300, 
		uri: "https://picsum.photos/200/200" }} />
</View>
```

#### Image props:
- blurRadius
```js
<Image 
	blurRadius = {10}
	source={{ 
		width:200, 
		height: 300, 
		uri: "https://picsum.photos/200/200" }} />
```
- loadingIndicatorSource
- fadeDuration
- resizeMode
- onLoad

### Touchables
-  **TouchableWithoutFeedback:** No visual feedback on touch
- **TouchableOpacity:** On press down, the opacity of the wrapped view is decreased, dimming it.
-  **TouchableHighlight:** On press down, the opacity of the wrapped view is decreased, which allows the underlay color to show through, darkening or tinting the view.
```js
<View style={styles.continer}>
	<Text>
		Hello World!
	</Text>
	<TouchableOpacity 
		onPress={handlePress}>
		<Image source={require('./assets/icon.png')} />
	</TouchableOpacity>
</View>
```

### Button

```js
<View style={styles.continer}>
	<Button 
		color="orange" 
		title="Click Me"
		onPress={handlePress} />
</View>
```
### Alert
```js
<View style={styles.continer}>
	<Button 
		color="orange" 
		title="Click Me"
		onPress={() => alert("Button Pressed")} />
		<Button  
		title="Click Me"
		onPress={() => Alert.alert("Title","Message",[{text: "Yes", onPress: ()=>console.log("yes")},
		{text: "No", onPress: ()=>console.log("yes")}]} />
</View>
```
**Alert Box with text prompt (Question):**
```js
<View style={styles.continer}>
	<Button  
		title="Click Me"
		onPress={() => Alert.prompt("Title","Message",text => console.log(text))} />
</View>
```

### Platform Specific Code:
```js
const  styles = StyleSheet.create({
	container: {
		flex: 1,
		backgroundColor: '#fff',
		alignItems: 'center',
		justifyContent: 'center',
		paddingTop: Platform.OS === "android" ? 20: 0,
	},
});
```
