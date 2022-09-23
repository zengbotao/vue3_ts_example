<script>
export default {
  props: ["modelValue"],
  emits: ["update:modelValue"],
};
// 1父组件v-model绑定
// 2子组件props中，用modelValue接受
// 3子组件绑定value值为modelValue，改变的时间出发emit方法,名字必须是'update:modelValue'
// 4 emits注册此方法
</script>

<template>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
