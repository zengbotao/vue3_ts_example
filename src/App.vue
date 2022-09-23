<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
    <setup></setup>
    <defineExpose ref="updatePwd"></defineExpose>
    <nonSet ref="sub" v-model="vd" :dd="fd" :msg="vd" @b="jieshou"></nonSet>
    <CustomInput v-model="message" /> {{ message }}{{ vd }}
  </nav>
  <router-view />
</template>
<script lang="ts">
import {
  defineComponent,
  ref,
  toRefs,
  reactive,
  getCurrentInstance,
  provide,
} from "vue";
import setup from "./views/setup.vue";
import nonSet from "./views/nonSet.vue";
import CustomInput from "./views/CustomInput.vue";
import defineExpose from "./views/defineExpose.vue";
export default defineComponent({
  components: { setup, nonSet, CustomInput, defineExpose },
  setup() {
    //可以将多个数据写在data里，然后统一差分
    let data = reactive({
      sd: "ffff",
      fd: "ffffffff",
      vd: "fsdfsdfs",
      date: { sfsdfsdf: "fdsfsdfsdfsd" },
    });
    let message = ref("hello");
    // provide函数必须在setup里，不可以放在函数内部
    provide("val_a", message);
    provide("val_a2", message);
    // provide(){
    //   return {
    //   "val_a": message
    //   }
    // }

    function jieshou(val: String): void {
      // 写事件注意写ts规范
      console.log(val, "jieshou");
      updatePasswordHandle();
      // testExpose();
    }

    // 定义组件ref的类型,获取实例加上接口更好点记得注册，updatePwd在setup下面注册
    const updatePwd = ref<InstanceType<typeof defineExpose>>();
    // 使用子组件的属性与方法,记得注册
    const updatePasswordHandle = () => {
      console.log(ref(), updatePwd, updatePwd.value?.dialogVisible);
      updatePwd.value?.cons(); //接受的方法要加value，（）才能运行
    };

    return {
      ...toRefs(data),
      message,
      jieshou,
      updatePasswordHandle,
      updatePwd,
    };
  },
});
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
