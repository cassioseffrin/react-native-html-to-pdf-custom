# react-native-html-to-pdf-custom

Compatible with React Native v0.60 and above. 

This is a customization of the official package https://github.com/christopherdro/react-native-html-to-pdf. 

This customization allows to create a pdf in specific size as described below:

let options = {
    html: var_with_html_content,
    fileName: 'nameOfFile.pdf',
    height: totalHeight, // ios
    width: totalWidth,  //ios
    page: {
        size: { mm: { h: totalHeight, w: totalWidth  } }, 
        orientation: 'Portrait'
    },
    base64: true //generate base64
};

## Installation

1. Run ` npm i react-native-html-to-pdf@git+https://git@github.com/cassioseffrin/react-native-html-to-pdf-custom.git --save`

### iOS

1. Inside the ios directory run: pod install. 

 
#### Android - Manual installation
- Edit `android/settings.gradle` to included

```java
include ':react-native-html-to-pdf-custom'
project(':react-native-html-to-pdf-custom').projectDir = new File(rootProject.projectDir,'../node_modules/react-native-html-to-pdf-custom/android')
```

- Edit `android/app/build.gradle` file to include

```java
dependencies {
  ....
  compile project(':react-native-html-to-pdf-custom')

}
```

- Edit `MainApplication.java` to include

```java
// import the package
import com.christopherdro.htmltopdf.RNHTMLtoPDFPackage;

// include package
new MainReactPackage(),
new RNHTMLtoPDFPackage()
```

## Usage
```javascript

import React, { Component } from 'react';
import { Text, TouchableHighlight, View } from 'react-native';
import { RNHTMLtoPDF } from 'react-native-html-to-pdf-custom';

export default class Example extends Component {
	async createPDF() {
		let options = {
			html: '<h1>PDF TEST</h1>',
			fileName: 'test',
			directory: 'docs',
			page: {
				size: 'UsLetter',
				orientation: 'Landscape'
			}
		};
		let file = await RNHTMLtoPDF.convert(options);
		// console.log(file.filePath);
		alert(file.filePath);
	}

	render() {
		return (
			<View style={{ flex: 1, justifyContent: 'center' }}>
				<TouchableHighlight onPress={this.createPDF}>
					<Text style={{ textAlign: 'center' }}>Create PDF</Text>
				</TouchableHighlight>
			</View>
		);
	}
}

```

## Options

| Param | Type | Default | Note |
|---|---|---|---|
| `html` | `string` |  | HTML string to be converted
| `fileName` | `string` | Random  | Custom Filename excluding .pdf extension
| `base64` | boolean | false  | return base64 string of pdf file (not recommended)

#### iOS Only

| Param | Type | Default | Note |
|---|---|---|---|
| `height` | number | 612  | Set document height points to US Letter, Landscape
| `width` | number | 792  | Set document width points to US Letter, Landscape
| `padding` | number | 10  | Outer padding (points)


##### Android Only

| Param | Type | Default | Note |
|---|---|---|---|
| `fonts` | Array | | Allow custom fonts `['/fonts/TimesNewRoman.ttf', '/fonts/Verdana.ttf']`
| `page` | JSON | | Allow custom page size `{page: { size: { mm: { h: totalHeight, w: totalWidth  } },  orientation: 'Portrait'}`


### Options: page

| Param | Type | Default | Note |
|---|---|---|---|
| `orientation` | `string` | Portrait | Landscape, Portrait
| `size` | `string` | UsLetter  | A0 - A8, UsGovernmentLetter, UsLetter, UsLegal
 