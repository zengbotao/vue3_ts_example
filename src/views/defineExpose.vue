// 子组件
<template>
  <div>defineExpose</div>
</template>
<script lang="ts" setup>
import {
  defineComponent,
  ref,
  toRefs,
  reactive,
  getCurrentInstance,
  provide,
} from "vue";
const dialogVisible = ref(false);
const cons = () => {
  console.log("记得注册");
};
// 导出父组件需要用的属性与方法
defineExpose({
  dialogVisible,
  cons,
});
</script>
