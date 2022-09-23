<template>
  <div class="about">
    <h1 @click="myFn">This is an about page{{ state }}</h1>
  </div>
</template>
<script setup lang="ts">
import { toRaw, reactive } from "vue";
import { useRoute, useRouter } from "vue-router";
import { useStore } from "vuex";

// 方法: 需要在setup里面执行
const route = useRoute();
const router = useRouter();
const store = useStore();

// store.commit
// route.params
// router.push
console.log(router.push, "第三方");
console.log(toRaw(router).currentRoute.value.fullPath); //获取当前路由
// toRaw使用场景,要从vue中引入
// ref/reactive数据类型每次修改都会被追踪，都会更新UI界面，
// 但是这样是非常消耗性能的，所以如果我们有一些操作不需要追踪，不需要更新UI界面，
// 可以通过toRaw方法拿到它的原始数据，对原始数据进行修改，
// 这样就不会被追踪，这样就不会更新UI界面，这样性能就好了。
let obj = { name: "lj", age: 18 };
let state = reactive(obj);
let obj2 = toRaw(state);
console.log(obj === obj2); //true
function myFn() {
  obj2.name = "zs";
  console.log(state); //Proxy {name: "zs", age: 18},但是显示的仍然是name: "lj"
  console.log(obj2); //{name: "zs", age: 18}
}
</script>
