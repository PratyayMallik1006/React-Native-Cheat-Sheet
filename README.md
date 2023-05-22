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

# Core Components and APIs
Refer to all components at: https://reactnative.dev/docs/components-and-apis
## View
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

## Text
```js
const handlePress = () => console,log("Text Pressed");

<View style={styles.continer}>
	<Text numberOfLines={1}
		onPress={handlePress}>
		Hello World!
	</Text>
</View>

```
## Images
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

### Image props:
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

## Touchables
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

## Button

```js
<View style={styles.continer}>
	<Button 
		color="orange" 
		title="Click Me"
		onPress={handlePress} />
</View>
```
## Alert
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

## Platform Specific Code:
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
# Layout
**Working with orientations: Portrait or Landscape**
1. Go to ProjectFile > App.json 
```js
"orientation":"default"
```
2. Open CMD
```
npm i @react-native-community/hooks
```
3.  ProjectFile > App.js
```js
export  default  function  App() {
	const  orientation = useDeviceOrientation();
	
	return (
		<View  style={{
			backgroundColor:"grey",
			width:"100%",
			height: orientation === "landscape" ? "100%" : "30%"
			}}>	
		</View>
	);
}
```
## Layout with Flexbox

- Read more at: https://reactnative.dev/docs/flexbox
- [`flex`](https://reactnative.dev/docs/layout-props#flex)  will define how your items are going to  **“fill”**  over the available space along your main axis. Space will be divided according to each element's flex property.
```js
return (
    //Parent Flex view
    <View
      style={
        {
          // Try setting `flexDirection` to `"row"`.
          flexDirection: 'column',
        }>
	   //Children Flex Views
      <View style={{flex: 1, backgroundColor: 'red'}} /> // 1/6th area
      <View style={{flex: 2, backgroundColor: 'darkorange'}} /> // 2/6th 
      <View style={{flex: 3, backgroundColor: 'green'}} /> // 3/6th
    </View>
  );
```

### Flex Direction

[`flexDirection`](https://reactnative.dev/docs/layout-props#flexdirection)  controls the direction in which the children of a node are laid out. This is also referred to as the main axis. The cross axis is the axis perpendicular to the main axis, or the axis which the wrapping lines are laid out in.

-   `column`  (**default value**) Align children from top to bottom. If wrapping is enabled, then the next line will start to the right of the first item on the top of the container.
    
-   `row`  Align children from left to right. If wrapping is enabled, then the next line will start under the first item on the left of the container.
    
-   `column-reverse`  Align children from bottom to top. If wrapping is enabled, then the next line will start to the right of the first item on the bottom of the container.
    
-   `row-reverse`  Align children from right to left. If wrapping is enabled, then the next line will start under the first item on the right of the container.

### Justify Content

[`justifyContent`](https://reactnative.dev/docs/layout-props#justifycontent)  describes how to align children within the main axis of their container. For example, you can use this property to center a child horizontally within a container with  `flexDirection`  set to  `row`  or vertically within a container with  `flexDirection`  set to  `column`.

-   `flex-start`(**default value**) Align children of a container to the start of the container's main axis.
    
-   `flex-end`  Align children of a container to the end of the container's main axis.
    
-   `center`  Align children of a container in the center of the container's main axis.
    
-   `space-between`  Evenly space off children across the container's main axis, distributing the remaining space between the children.
    
-   `space-around`  Evenly space off children across the container's main axis, distributing the remaining space around the children. Compared to  `space-between`, using  `space-around`  will result in space being distributed to the beginning of the first child and end of the last child.
    
-   `space-evenly`  Evenly distribute children within the alignment container along the main axis. The spacing between each pair of adjacent items, the main-start edge and the first item, and the main-end edge and the last item, are all exactly the same.
