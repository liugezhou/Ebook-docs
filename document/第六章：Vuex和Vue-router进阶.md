#### 6.1 vuex实现原理讲解
> 通过一个案例来学习源码中的实现思路：Vuex的原理关键：使用Vue实例管理状态  
```
<div id="root">{{data}}</div>
    <div id="root2">{{data2}}</div>
    <div id="root3">
      <button @click="change">change</button>
</div>
……

function registerPlugin(Vue){
    const Vuex = {
    Vue._vm = new Vue({
        data:{
            message:'Hello World'
        }
    })
}
new Vue({
    el: '#root',
    computed: {
        data() {
            return this.$store.state.messge
        }
    }
})
new Vue({
    el: '#root2',
    computed: {
        data() {
            return this.$store.state.messge
        }
    }
})
new Vue({
    el: '#root3',
    methods: {
        change(){
            const newValue = this.$store.state.message + '.'
            this.$store.mutations.setMessage(newValue)
        }
    }
})
```