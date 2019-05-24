# vuex是什么
每一个 Vuex 应用的核心就是 store（仓库）
store 基本上就是一个容器，它包含着你的应用中大部分的状态 (state)

1、Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

2、你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。

# 使用场景

https://juejin.im/post/5a3e0fa05188252103347507

# 开始

    step 1 创建文件 store/store.js

    step 2 写入
    import Vuex from 'vuex'
    import Vue from 'vue'
    Vue.use(Vuex)
    const store = new Vuex.Store({
        state: {
            count: 0
        },
        mutations: {
            increment (state) {
                state.count++
            }
        }
    })

    export default store

    step 3 可在组件中 调用
    import store from '../store/store.js'
    store.commit('increment')
    
## 单一状态树
    用一个对象就包含了全部的应用层级状态 每个应用将仅仅包含一个 store 实例。单一状态树让我们能够直接地定位任一特定的状态片段，在调试的过程中也能轻易地取得整个当前应用状态的快照。

## 在vue组件中 使用vuex
    vuex的存储是响应式的 读取store的状态  通过计算属性
    computed: {
    count () {
      return store.state.count
        }
    }
    每当 store.state.count 变化的时候, 都会重新求取计算属性，并且触发更新相关联的 DOM。
把store对象注入到实例中 store注入到所有子组件中

    store
    Components: ...
通过子组件访问 

    this.$store.state.count

## mapState 辅助函数
作用  当一个组件需要获取多个状态时， 这些状态都声明到计算属性中  会有重复和冗余 为了 避免这种情况  就使用 mapState函数 

    import { mapState } from 'vuex'
    export default {
         computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
    })
    }
当计算属性与state子节点名称同名时 传入一个字符串即可

    computed: mapState([
        // 等价于 count : store.state.count
        'count'
    ])

对象展开运算符  mapState函数返回的是一个对象
    
    computed: {
    localComputed () { /* ... */ },
    // 使用对象展开运算符将此对象混入到外部对象中
    ...mapState({
        // ...
    })
    }


# Getter

有时候我们需要从 store 中的 state 中派生出一些状态，例如对列表进行过滤并计数：

    computed: {
    doneTodosCount () {
        return this.$store.state.todos.filter(todo => todo.done).length
    }
    

mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性：

    import { mapGetters } from 'vuex'

    export default {
    // ...
    computed: {
    // 使用对象展开运算符将 getter 混入 computed 对象中
        ...mapGetters([
        'doneTodosCount',
        'anotherGetter',
        // ...
        ])
    }
    }
    mapGetters({
    // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
    doneCount: 'doneTodosCount'
    })

# Mutation

使用 mutation 改变state状态 

mutation 修改state状态 同步修改 遵循规则 

1 状态 尽量在store中声明完成

2 当需要新的变量时

# action


# Module 

const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态