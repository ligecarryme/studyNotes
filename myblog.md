## quasar-frontWeb

v-ripple  使其变成可点击的组件

## element-admin

### 用户登录 ———2020-10-2

axios配置，解决跨域问题，使用 Json 传递数据   

```js
//vue.config.js
module.exports = {
    devServer: {
        proxy: {
            '/api':{
                target: 'http://localhost:8079',
                ws: true,
                changeOrigin: true, //开启跨域请求
                pathRewrite:{
                    '^api': ''
                }
            }
        }
    },
    publicPath: '/admin',
}
//axios配置
axios.defaults.baseURL = "http://localhost:8079/admin";
axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';
axios.defaults.headers.post['Content-Type'] = 'application/json';
axios.defaults.withCredentials= true;
```

是否能跨域请求主要取决于后端

#### axios 请求带参数

https://www.cnblogs.com/yiyi17/p/9409249.html post解释的很清楚

```js
// get
// 为给定 ID 的 user 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 上面的请求也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

//post  json
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
// form-data
let data = new FormData（）;
data.append（'code'，'1234'）;
data.append（'name'，'yyyy'）;
axios.post（`$ {this。$ url} / test / testRequest`，data）.then（res => {
console.log（'res =>'，res）;
}）

// x-www-form-urlencoded
import axios from 'axios' 
import qs from 'Qs' 
let data = {"code":"1234","name":"yyyy"}; axios.post(`${this.$url}/test/testRequest`,qs.stringify({ data })) .then(res=>{ console.log('res=>',res); })
```

#### 刷新页面的三种方式

1. v-if hack

```vue
<template>
  <my-component v-if="renderComponent" />
</template>
<script>
  export default {
    data() {
      return {
        renderComponent: true,
      };
    },
    methods: {
      forceRerender() {
        // 从 DOM 中删除 my-component 组件
        this.renderComponent = false;
        
        this.$nextTick(() => {
          // 在 DOM 中添加 my-component 组件
          this.renderComponent = true;
        });
      }
    }
  };
</script>
```

2. forceUpdate（最简洁）

```js
// 全局
import Vue from 'vue';
Vue.forceUpdate();

// 使用组件实例
export default {
  methods: {
    methodThatForcesUpdate() {
      // ...
      this.$forceUpdate();
      // ...
    }
  }
}
```

3. 修改组件的key达到组件重新渲染（最好）

```vue
<template>
  <component-to-re-render :key="componentKey" />
</template>
<script>
export default {
  data() {
    return {
      componentKey: 0,
    };
  },
  methods: {
    forceRerender() {
      this.componentKey += 1;  
    }
  }
}
</script>
```

#### quasar滚动区域

因为是聊天区，所以每次刷新滚动条都要在底部，实现方法：

```vue
<template>
    <q-scroll-area ref="chatArea" @scroll="scrollinfo" >
          <div v-for="(item,index) of message" :key="item.id">
             <q-chat-message :name="item.nickname" :text="[item.content]" :stamp="item.createTime" />
           </div>
        <q-scroll-observer /> <!-- 监控滑动区域，主要监控滑动条的长度。绑定scroll方法 -->
    </q-scroll-area>
</template>
<script>
export default {
	data(){
        return {
			scrollsize: 0;
        }
    },
    watch:{ // 监控滚动条的变化
        scrollsize: function(val){
      		this.$refs.chatArea.setScrollPosition(val-500,100); //设置到底部500是我自己设置的聊天区域高度 
    	}
    }，
    scrollinfo(info){ 
      const size = info.verticalSize;
      this.scrollsize = size;
    }
}
</script>
```

