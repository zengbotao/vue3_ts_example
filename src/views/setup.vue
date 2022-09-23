<template>
  <div>
    <div>{{ num }} {{ name }} {{ age }}</div>
  </div>
</template>

<script lang="ts">
import { ref, reactive, toRefs, defineComponent } from "vue";
export default defineComponent({
  setup() {
    const num = ref(1);
    const user = reactive({
      name: "Jack",
      age: 12,
    });
    const { name, age } = toRefs(user);
    return {
      num,
      name,
      age,
    };
  },
});
</script>

<style scoped></style>
