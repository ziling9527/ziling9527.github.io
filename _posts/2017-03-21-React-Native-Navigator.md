---
layout: post
title:  React Native Navigator
date:   2017-03-21 14:14:00
categories: ReactNative
tags: ReactNative
---
###### 1、index.android.js
```javascript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */
import React, {Component} from 'react';
import {
    AppRegistry,
    View,
    Navigator,
    Text,
    BackAndroid,
    StyleSheet,
    ToolbarAndroid,
    TouchableHighlight
} from 'react-native';
import Login from './components/Login';

var _navigator;// 全局变量
BackAndroid.addEventListener('hardwareBackPress', () => {
    if (_navigator && _navigator.getCurrentRoutes().length > 1) {
        _navigator.pop();
        return true;
    }
    return false;
});

// 控制页面如何跳转的总枢纽
let RouteMapper = function (route, navigationOperations) {
    _navigator = navigationOperations;
    let Component_ = route.component;
    if(Component_){
        return <Component_ {...route.params} navigator={_navigator}/>
    }
};

export default class Home extends Component {
    render() {
        let firstPageRouter = 'login';
        let firstComponent = Login;
        return (
            <Navigator
                style={styles.container}
                initialRoute={{name: firstPageRouter,component:firstComponent}}
                renderScene={RouteMapper}
            />
        );
    }
}

var styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#593012',
    },
});

AppRegistry.registerComponent('Home', () => Home);

```

######2、Login.js
```javascript
/**
 * Created by Administrator on 2017/2/23.
 */
import React, {Component, PropTypes} from 'react';

import {
    AppRegistry,
    View,
    Navigator,
    Text,
    BackAndroid,
    StyleSheet,
    ToolbarAndroid,
    TouchableHighlight
} from 'react-native';

import MainScene from './MainScene';

export default class Login extends Component {

    static defaultProps = {
        navigator:null,
    }

    constructor(props) {
        super(props);
        this.state = {
            user : null,
        }
    }

    login(){
        let this_ = this;
        this.props.navigator.push({
            name: 'main',
            component:MainScene,
            params:{//传给其他页面的参数,这些个参数是作为props传给下个页面的
                title: '这是从登录跳转而来',
                id : 1,
                // 为了获取下个页面返回给这个页面的数据，这里使用了一个回调函数
                getUser:function (user) {
                    this_.setState({
                        user:user,
                    });
                }
            },
        });
    }

    render() {
        if(this.state.user){
            return(
                <View>
                    <Text style={{fontSize:50}}>
                        用户信息: { JSON.stringify(this.state.user) }
                    </Text>
                </View>
            );
        }else {
            return (
                <View>
                    <TouchableHighlight style={{margin: 50}} onPress={this.login.bind(this)}>
                        <Text style={{width: 100, height: 60,fontSize:50}}>
                            登录
                        </Text>
                    </TouchableHighlight>

                    <TouchableHighlight style={{margin: 50}}>
                        <Text style={{width: 100, height: 60,fontSize:50}}>
                            注册
                        </Text>
                    </TouchableHighlight>
                </View>
            );
        }
    };
}
```

######3、MainScene.js
```javascript
/**
 * Created by Administrator on 2017/2/23.
 */
import React, {Component, PropTypes} from 'react';

import {
    AppRegistry,
    View,
    Navigator,
    Text,
    BackAndroid,
    StyleSheet,
    ToolbarAndroid,
    TouchableHighlight
} from 'react-native';


const USER = {
    1: {name : "lxr",age : 39},
    2: {name : "zbs",age : 67},
};

let onActionSelected = function (position) {
    if (position == 0) {
        console.log("===============> 患者列表")
    } else if (position == 1) {
        console.log("===============> 电子病历")
    }
}

let onIconClick = function () {
    console.log("===============> onIconClick")
}

export default class MainScene extends Component {

    static defaultProps = {
        title: null,
        navigator:null,
    }

    constructor(props) {
        super(props);
    }

    toBack(){
        const id_ = this.props.id;
        const getUser = this.props.getUser;
        if(id_ && getUser){
            let user = USER[id_];
            getUser(user);
        }
        if(this.props.navigator){
            this.props.navigator.pop();
        }
    }

    render() {
        return (
            <View style={{flex: 1}}>
                <ToolbarAndroid
                    logo={require('./../imgs/test.png')}
                    navIcon={require('./../imgs/01_deault.png')}
                    title={this.props.title}
                    titleColor="white"
                    actions={[
                        {
                            title: '患者列表',
                            icon: require('./../imgs/02_deault.png'),
                            show: 'always',
                            showWithText: false
                        },
                        {
                            title: '电子病历',
                            icon: require('./../imgs/03_deault.png'),
                            show: 'always',
                            showWithText: false
                        }
                    ]}
                    style={styles.toolbar}
                    onActionSelected={onActionSelected}
                    onIconClicked={onIconClick}// 这个是作用在navIcon选项上的
                />
                <TouchableHighlight style={{flex:1}} onPress={this.toBack.bind(this)}>
                    <Text style={{width: 600, height: 300,fontSize:50}}>
                        点击我返回上一个页面，携带有参数。
                    </Text>
                </TouchableHighlight>
            </View>
        );
    };
}

var styles = StyleSheet.create({
    toolbar: {
        backgroundColor: '#666666',
        height: 56,
    },
});
```
######4、参考资料
1、[ReactNative官方文档](https://facebook.github.io/react-native/docs/using-navigators.html)
2、[ReactNative 中文文档](https://reactnative.cn/docs/0.41/using-navigators.html#content)
3、[新手理解Navigator的教程](http://bbs.reactnative.cn/topic/20/%E6%96%B0%E6%89%8B%E7%90%86%E8%A7%A3navigator%E7%9A%84%E6%95%99%E7%A8%8B)