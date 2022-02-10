---
title: "Learn React 07"
date: 2022-02-10T10:15:45+08:00
draft: false
tags: [React]
categories: [React]
---

> 消息订阅-发布机制

#### React中兄弟组件或深层次组件之间的通信

1. 工具库：[PubSubJS](https://github.com/mroderick/PubSubJS)
2. 下载：npm i pubsub-js --save
3. 使用：
   - import PubSub from 'pubsub-js' //引入
   - PubSub.subscribe('delete', function(data){ }); //订阅消息
   - PubSub.publish('delete', data) //发布消息

#### List组件订阅消息

```jsx
componentDidMount(){
  this.token = PubSub.subscribe('searchData',(_,stateObj)=>{
      this.setState(stateObj)
  })
}
componentWillUnmount(){
  PubSub.unsubscribe(this.token)
}
```

#### Search组件发布消息

```jsx
PubSub.publish('searchData',{isLoading:false,users:response.data.items})
```

