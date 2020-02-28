#### 3.1 $emit和$on 
> 主要解决的问题是事件的定义和消费. 
> 通过源码学习可以知道$on可以绑定多个事件名称，以及多个事件。
```
<html>
  <head>
    <title>$emit 和 $on</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  </head>
  <body>
   <div id="app">
       <button @click="show">Click Me!</button>
   </div>
   <script>
       new Vue ({
           el : '#app',
           data () {
               return {
                   msg: 'Welcome to visit:'
               }
           },
           created () {
               this.$on('website',this.showwebsite)
           },
           methods: {
            showwebsite(e){
                console.log(this.msg, e)
            },
            show() {
                this.$emit('website','https://www.liugezhou.online')
            }
           }
       })
   </script>
  </body>
</html>
```

#### 3.2 directive
```
 Vue.directive('loading',function update(el,binding,vnode) {
                 if(binding.value){
                    const div= document.createElement('div')
                    div.innerText = '加载中……',
                    div.setAttribute('id','loading')
                    div.style.position = 'absolute'
                    div.style.left = 0
                    div.style.top = 0
                    div.style.width = "100%"
                    div.style.height = "100%"
                    div.style.display = 'flex'
                    div.style.justifyContent = 'center'
                    div.style.alignItems = 'center'
                    div.style.color = 'white'
                    div.style.background = 'rgba(0,0,0,.7)'
                    document.body.append(div)
                 }else{
                     const div = document.getElementById('loading')
                     div && document.body.removeChild(document.getElementById('loading'))
                 }
         })
         new Vue ({
             el : '#app',
             data () {
                 return {
                  isLoading:false,
                     msg: ''
                 }
             },
             methods: {
              login() {
                  this.isLoading = !this.isLoading
                  this.msg = 'welcome!'
                  setTimeout(() => {
                      this.isLoading = !this.isLoading
                  },3000)
              }
             }
         })
```

#### 3.3 Vue componenet 
```
 Vue.component('Test',{
                template :'<div>{{msg}}</div>',
                props: {
                    msg : {
                        type:String,
                        default: 'Hello World!'
                    }
                }
            })
            new Vue({
                el: '#root',
                data() {
                    return {
                        messge:'Component'
                    }
                } 
            })
```

#### 3.4 Vue extend用法
```
  const component = Vue.extend({
                template :'<div>{{msg}}</div>',
                props: {
                    msg : {
                        type:String,
                        default: 'Hello World!'
                    }
                }
            })
            Vue.component('Test',component)
            new Vue({
                el: '#root',
                data() {
                    return {
                        messge:'Component'
                    }
                } 
            })
```

#### 3.5 Vue.extend 进阶用法
```

```

#### 3.6 Vue.use用法