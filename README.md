# RNTipsView

you can draw on the view, and cut an image.

![](https://github.com/MagicalYan/RNTipsView/blob/master/snapshot.gif?raw=true)

# Support

iOS only

# Install
npm i --save react-native-tipsview

# Usage
## Founction:

export: cut the TipsView, return the uri.

clear: clear the view that you drew.

## properties:
lineWidth: line width.

lineColor: line color.

cacheType: 0,default save image data to tmp, back tmp image file path. 1, save image to cache, back base64 string.

# Example

```
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Image,
  TouchableOpacity,
  ImageStore
} from 'react-native';
import TipsView from 'react-native-tipsview';

export default class tips extends Component {
  constructor(props) {
    super(props);
    this.state = {
      imageURI:'',
    };
  }
  render() {
    return (
      <View style={styles.container}>
        <TipsView ref='tipsView' lineColor='red' cacheType={1} lineWidth={8} style={styles.tipsViewStyle}>
          {
            this.state.imageURI.length > 0 ? (
              <Image source={{uri:this.state.imageURI}} style={styles.previewStyle}/>
            ) : null
          }
        </TipsView>
        <TouchableOpacity onPress={()=>{
          this.refs.tipsView.clear();
          this.setState({imageURI:''});
        }}>
          <Text style={styles.text}>{'clear'}</Text>
        </TouchableOpacity>

        <TouchableOpacity onPress={()=>{
          this.refs.tipsView.export().then(result=>{
            this.setState({imageURI:result});
          }, error=>{
            console.warn(error);
          });
        }}>
          <Text style={styles.text}>{'cut'}</Text>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  tipsViewStyle: {
    flex:1,
    backgroundColor:'white',
  },
  previewStyle: {
    position:'absolute',
    width: 100,
    height: 100,
    resizeMode:'contain',
  },
  container: {
    flex: 1,
    backgroundColor: '#F5FCFF',
  },
  text: {
    alignSelf: 'center',
    padding: 20,
  }
});

AppRegistry.registerComponent('tips', () => tips);
```
