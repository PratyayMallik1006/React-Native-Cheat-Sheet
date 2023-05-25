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

# Styling
## Border
```js
return (
	<View
		style={{
			flex: 1,
			justifyContent:"centre",
			alignItems:"center",
			>
			<View 
				style={{
					backgroundColor: "#333",
					width:100,
					height:100,
					borderWidth:10,
					borderColor:"#eee",
					borderRadius: 10,
					borderTopWidth:20,
					borderTopLeftRadius:50,
					}}>
		</View>
			
);
```
## shadow
1. IOS
```js
return (
	<View
		style={{
			flex: 1,
			justifyContent:"centre",
			alignItems:"center",
			>
			<View 
				style={{
					backgroundColor: "#333",
					width:100,
					height:100,
					shadowColor: "grey",
					shadowOffset:{width: 10, heigth: 10}.
					shadowOpacity:1,
					shadowRadius: 10,
					}}>
		</View>
			
);
```
2. Android
```js
return (
	<View
		style={{
			flex: 1,
			justifyContent:"centre",
			alignItems:"center",
			>
			<View 
				style={{
					backgroundColor: "#333",
					width:100,
					height:100,
					elevation: 10,
					}}>
		</View>
			
);
```
## Adding Padding Under StatusBar 
1. Using Platform
```js
import {
FlatList,
SafeAreaView,
StyleSheet,
Platform,
StatusBar,
} from  "react-native";

function  userScreen(props) {
return (
<SafeAreaView  style={styles.screen}>
<FlatList
data={messages}
keyExtractor={(message) =>  message.id.toString()}
renderItem={({ item }) => (
<ListItem
title={item.name}
subTitle={item.bio}
image={item.image}
/>
)}
/>
</SafeAreaView> ); }  

const  styles = StyleSheet.create({
screen: {
paddingTop: Platform.OS === "android" ? StatusBar.currentHeight : 0,
},
});
```

2. Using expo Constants
- npm i expo-constants
```js
import  Constants  from  "expo-constants";
const  styles = StyleSheet.create({
screen: {
paddingTop:Constants.statusBarHeight,
},
});
```
# FlatList

A performant interface for rendering basic, flat lists, supporting the most handy features:

-   Fully cross-platform.
-   Optional horizontal mode.
-   Configurable viewability callbacks.
-   Header support.
-   Footer support.
-   Separator support.
-   Pull to Refresh.
-   Scroll loading.
-   ScrollToIndex support.
-   Multiple column support.
```js
const DATA = [
  {
    id: 1,
    title: 'First Item',
  },
  {
    id: 2,
    title: 'Second Item',
  },
  {
    id: 3,
    title: 'Third Item',
  },
];

const Item = ({title}) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);

const App = () => {
  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        renderItem={({item}) => <Item title={item.title} />}
        keyExtractor={item => item.id.toString()}
      />
    </SafeAreaView>
  );
};
```
# Expo Gesture Handler
Read more: https://docs.swmansion.com/react-native-gesture-handler/
1. Install library
```
npx expo install react-native-gesture-handler
```
2. Implement
```js
import  Swipeable  from  'react-native-gesture-handler/Swipeable';

function  Gesture(props) {

	const  swipeLeft = () => {
		<View style={{
			backgroundColor:"red",
			width:70,
			}}>
		</View>
	};

	return  (  
	<Swipeable renderLeftActions={swipeLeft}>  
	<Text>"hello"</Text>  
	</Swipeable>  
	);
}
```
# Pull To Refresh
```js
import  React, { useState } from  "react";
import { FlatList, StyleSheet, View } from  "react-native";


const  originalList = [
  {
    id: 1,
    title: 'First Item',
  },
  {
    id: 2,
    title: 'Second Item',
  },
];

function  Refreshing(props) {
const [list, setList] = useState(originalList);
const [refreshing, setRefreshing] = useState(false);

return (
<View>
<FlatList
data={list}
keyExtractor={(l) =>  l.id.toString()}

refreshing={refreshing}
onRefresh={() => {
setList([
  {
    id: 1,
    title: 'First Item',
  },
  {
    id: 2,
    title: 'Second Item',
  },
  {
    id: 3,
    title: 'Third Item',
  },
]);
}}
/>
</View>
);
}
```

# Input
## TextInput
```js
const[name, setName]=useState('');
<TextInput 
	onChangeText={text=>setName(text)}
	placeholder="Enter Your Name"
	//keyboardType="numeric"
	//secureTextEntry={true}
/>
```
## Switch
```js
const[isDark, setIsDark]=useState(false);
<Switch 
	value={isDark} onValueChange={newValue => setIsDark(newValue)}
/>
```
## Picker
```js
function  CustomPicker() {

const items= [
  {
    id: 1,
    title: 'First Item',
  },
  {
    id: 2,
    title: 'Second Item',
  },
  {
    id: 3,
    title: 'Third Item',
  },
];
const placehoder="Categories";

const [modalVisible, setModalVisible] = useState(false);
const [category, setCategory] = useState(items[0]);
const selectedItem =  category;

const onSelectItem={(item) =>  setCategory(item)}

return (
<>
	<TouchableWithoutFeedback  onPress={() =>  setModalVisible(true)}>
		<View>
		<Text  style={styles.text}>
		{selectedItem ?  selectedItem.label : placeholder}
		</Text>
		<MaterialCommunityIcons name="chevron-down" />
		</View>
	</TouchableWithoutFeedback>
	<Modal  visible={modalVisible}  animationType="slide">
		<Button  title="Close"  onPress={() =>  setModalVisible(false)}  />
		<FlatList
			data={items}
			keyExtractor={(item) =>  item.id.toString()}
			renderItem={({ item }) => (
			
			<TouchableOpacity  onPress={() => {
				setModalVisible(false);
				onSelectItem(item);}>
				<Text>{item.label}</Text>
			</TouchableOpacity>
		)}
		/>
	</Modal>
</>
);
}
```
# Forms
```js
function Login(){
const [email,setEmail] = useState();
const [password,setPassword] = useState();

return(
	<View>
		<TextInput 
			autoCapitalize="none"
			autoCorrect={false}
			keyboardType="email-address"
			onChangeText={(text) => setEmail(text)}
			placeholder="Email"
			textContentType="emailAddress" // for IOS autofill
		/>
		<TextInput 
			autoCapitalize="none"
			autoCorrect={flase}
			onChangeText={(text) => setPassword(text)}
			placeholder="Password"
			secureTextEntry={true}
			textContentType="password" // for IOS autofill
		/>
		<Button onPress={()=> console.log(email, password)} />
	</View>
)
}
```
## Forms Using Formik library
State variables no longer required
1. Install
```
npm i formik
```
2. Implement
```js
import { Formik } from 'formik'
function Login(){

return(
	<View>
		<Formik 
			intialValues={{email:'',password:''}}
			onSubmit={values => console.log(values)}
		>
			{({handleChange, handleSubmit}) =>(
				<>
					<TextInput 
						autoCapitalize="none"
						autoCorrect={false}
						keyboardType="email-address"
						onChangeText={handleChange("email")}
						placeholder="Email"
						textContentType="emailAddress" // for IOS autofill
					/>
					<TextInput 
						autoCapitalize="none"
						autoCorrect={flase}
						onChangeText={handleChange("password")}
						placeholder="Password"
						secureTextEntry={true}
						textContentType="password" // for IOS autofill
					/>
					<Button onPress={handleSubmit} />
				</>
			) }
		</Formik>
		
	</View>
)
}
```
## Validation Using Yup
1. Installation
```
npm i yup
```
2. Implementation
```js
import { Formik } from 'formik'
import * as Yup from 'yup';

const schema = Yup.Object().shape({
	email: Yup.string().required().email().label("Email"),
	password: Yup.string().required().min(8).label("Password"),
});

function Login(){

return(
	<View>
		<Formik 
			intialValues={{email:'',password:''}}
			onSubmit={values => console.log(values)}
			validationSchema={schema}
		>
			{({handleChange, handleSubmit, errors}) =>(
				<>
					<TextInput 
						autoCapitalize="none"
						autoCorrect={false}
						keyboardType="email-address"
						onChangeText={handleChange("email")}
						placeholder="Email"
						textContentType="emailAddress" // for IOS autofill
					/>
					<Text>{errors.email}</Text>
					<TextInput 
						autoCapitalize="none"
						autoCorrect={flase}
						onChangeText={handleChange("password")}
						placeholder="Password"
						secureTextEntry={true}
						textContentType="password" // for IOS autofill
					/>
					<Text>{errors.password}</Text>
					<Button onPress={handleSubmit} />
				</>
			) }
		</Formik>
		
	</View>
)
}
```
