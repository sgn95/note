
iview 按需引入

新建文件夹 iview/index.js 

    import { Card, Button, Table, Menu, Row, Col, Icon, Input, Select, Option, Modal, MenuItem, MenuGroup, Submenu, Tabs, TabPane, Radio, RadioGroup } from 'iview'
    const iview = {
    install: function (Vue) {
        Vue.component('Card', Card)
        Vue.component('Button', Button)
        Vue.component('Table', Table)
        Vue.component('Menu', Menu)
        Vue.component('Submenu', Submenu)
        Vue.component('MenuGroup', MenuGroup)
        Vue.component('MenuItem', MenuItem)
        Vue.component('Row', Row)
        Vue.component('Col', Col)
        Vue.component('Icon', Icon)
        Vue.component('Input', Input)
        Vue.component('Select', Select)
        Vue.component('Option', Option)
        Vue.component('Modal', Modal)
        Vue.component('Tabs', Tabs)
        Vue.component('TabPane', TabPane)
        Vue.component('Radio', Radio)
        Vue.component('RadioGroup', RadioGroup)
        }
    }
    export default iview

在main.js中添加 

    import iView from './iview' // 导入组件库
    import 'iview/dist/styles/iview.css'
    Vue.use(iView)

在.babelrc 文件中添加

     "plugins": ["transform-vue-jsx", "transform-runtime", ["import", {
    "libraryName": "iview",
    "libraryDirectory": "src/components"
    }]],


