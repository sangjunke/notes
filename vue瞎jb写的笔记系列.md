## vueX
### 安装
* npm install vuex --save
### 使用
```javascript
//在main.js中引入
import vuex from 'vuex'
Vue.use(vuex)
var store=new vuex.Store({
    state:{
        show:false
    }
})
//在 实例化VUe对象时加入store对象
new Vue({
    el:'#app',
    router,
    store,//使用store
    template:'<App>',
    components:{App}
})
```
### 为了方便，新建store文件，新建index.js文件，分开管理,index.js:
```javascript
import Vue from 'vue'
import vuex from 'vuex'
Vue.use(vuex)
export default new vuex.store({
    state:{
        show:false
    }
})
//main.js修改为：
import store from './store'
new Vue({
    el:'#App',
    router,
    store,
    template:'<App/>'
    components:{App}
})
```
### modules：如果状态过多，需要使用vuex的modules
```javascript
///导入
import appData from './app-data'
//
const store = new Vuex.Store({
	strict: debug,
  state,
  mutations,
	modules: {
		appData,//使用
		appHome,//使用
        other:other,//其他组件
	}
})

export default store //将接口暴露出去
```
### mutations：如果进行一个操作，需要依赖很多状态，使用 mutations
```javascript
export default {
    state:{//state
        show:false
    },
    mutations:{
        switch_dialog(state){//这里的state对应着上面这个state
            state.show = state.show?false:true;
            //你还可以在这里执行其他的操作改变state
        }
    }
//使用 $store.commit('switch_dialog') 来触发 mutations 中的 switch_dialog 方法。
```
### 注意：
* 使用 $store.commit('switch_dialog') 来触发 mutations 中的 switch_dialog 方法。
* mutations里的操作必须是同步的。
### action：多个 state 的操作 , 使用 mutations 会来触发会比较好维护 , 那么需要执行多个 mutations 就需要用  action
```javascript
export default {
    state:{//state
        show:false
    },
    mutations:{
        switch_dialog(state){//这里的state对应着上面这个state
            state.show = state.show?false:true;
            //你还可以在这里执行其他的操作改变state
        }
    },
    actions:{
        switch_dialog(context){//这里的context和我们使用的$store拥有相同的对象和方法
            context.commit('switch_dialog');
            //你还可以在这里触发其他的mutations方法
        },
    }
}
使用 $store.dispatch('switch_dialog') 来触发 action 中的 switch_dialog 方法。
```
