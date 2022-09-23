<template>
  <div>
    <input
      :value="msg"
      @input="$emit('update:modelValue', $event.target.value)"
    />
    <span>input是单标签，别写错了</span>
    <div>{{ num }} {{ name }} {{ age }}</div>
    <button @click="name = 'rose'">改名字</button>
    <button @click="fashe">发射</button>
    <provideInject></provideInject>
  </div>
</template>

<script setup lang="ts">
import {
  ref,
  reactive,
  toRefs,
  defineComponent,
  onMounted,
  inject,
  provide,
  computed,
  watch,
} from "vue";
import { useRoute, useRouter } from "vue-router";
import { useStore } from "vuex";
import provideInject from "@/views/test/provideInject";
// 方法: 需要在setup里面执行
const route = useRoute();
const router = useRouter();
const store = useStore();
defineComponent({ provideInject });
//props内部参数不用再次申明和使用
let props = defineProps({
  msg: String,
  dd: String,
  modelValue: String,
});

let fns = defineEmits(["update:modelValue", "b"]);
// attrs,emit,slots,expose 无需引入 直接使用defineXxx
// store.commit
// route.params
// router.push

function fashe() {
  fns("b", "b事件的数据");
}

// 基本
const num = ref(1);
// 引用的
const user = reactive({
  name: "Jack",
  age: 12,
});
const { name, age } = toRefs(user);
</script>

<style scoped></style>
