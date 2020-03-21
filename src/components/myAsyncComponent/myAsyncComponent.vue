<template>
  <div class="myAsyncComponent">
    <myAsyncCom1></myAsyncCom1>
    <myAsyncCom2></myAsyncCom2>
    <myAsyncCom3></myAsyncCom3>
    <myAsyncCom4></myAsyncCom4>
    <myAsyncCom5></myAsyncCom5>
    <myCom></myCom>
  </div>
</template>

<script>
import myLoading from './myLoading'
import myError from './myError'

let myCom = () =>({
  component: import('./myCom'),//加载成功时的组件
  loading:myLoading,//加载过程中的组件
  error:myError,//加载失败时的组件
  timeout:5000, //超时(超过该时长就加载error组件)
  delay:100 //延迟加载
})



import myAsyncCom1 from './myAsyncCom1' //加载组件方式1,步骤1
let myAsyncCom3= ()=> import('./myAsyncCom3')//异步加载组件 加载组件方式2
let myAsyncCom5= resolve =>require(['./myAsyncCom5'],resolve)//异步加载组件 加载组件方式3

export default {
  name: 'myAsyncComponent',
  data () {
    return {
      msg: 'myAsyncComponent'
    }
  },
  components:{
    myAsyncCom1,// //加载组件方式1,步骤2,
    myAsyncCom2:() => import ('./myAsyncCom2'),//异步加载组件 加载组件方式2
    myAsyncCom3,
    myAsyncCom4:resolve=>require(['./myAsyncCom4'],resolve),//异步加载组件 加载组件方式3
    myAsyncCom5,
    myCom
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
