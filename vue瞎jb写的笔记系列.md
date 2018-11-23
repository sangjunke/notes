## vue脚手架
### vue-cli 3.0使用
1. 安装node.js,8以上版本。 node:/官网/https://nodejs.org/zh-cn/
2. node -v 检测node版本
3. npm install -g @vue/cli or yarn global add @vue/cli
4. vue -V 检测vue-cli版本
5. vue create app //创建名为app的项目
6. Please pick a preset :(Use arrow keys)
..这里如果你是第一次用3.0版本的话,是没有前两个的，而只有最后两个，这里是让你选的，第一个是默认配置，一般选第二个，自己配置，这里选最后一个
7. Check the features needed for your project:
..当你选择后会出现上面图上的东西，这里你可以自由选择用哪些配置，按上下键选择哪一个，按空格键确定，所有的都选择好后，按enter键进行下一步，这里演示，我随便选了几个。
8. Pick a linter / formatter config: (Use arrow keys)
..上面这个是问你选择哪个自动化代码格式化检测，配合vscode编辑器的Prettier - Code formatter插件，我选的随后一个。
9. Pick additional lint features: 
..这里第一个选项是问你是否保存刚才的配置，选择确定后你下次再创建新目就有你以前选择的配置了，不用重新再配置一遍了。
10. Where do you prefer placing config for Babel, PostCSS, ESLint, etc(Usearrowkeys) ..上边这俩意思问你像，babel,postcss,eslint这些配置文件放哪？第一个是：放独立文件放置第二个是：放package.json里这里推荐放单独配置文件，选第一个。
11.  Save this as a preset for future projects? (y/N) 
..是否将以上这些将此保存为未来项目的预配置吗。
12. Save preset as: //项目描述。
13. cd app //进入项目。
14. npm run serve 启动项目。
15. npm run build 打包项目。
16. 3.0 可以新建一个vue.config.js文件 进行项目配置
## vue-cli3.0结构目录
* ![图片](https://upload-images.jianshu.io/upload_images/12471895-f9da4ac0459ebc0e.png)
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
