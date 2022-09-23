<template>
  <div>注入provide{{ val }}{{ val2 }}</div>
</template>

<script setup lang="ts">
import { ref, reactive, toRefs, onMounted, inject, computed, watch } from "vue";

let val = inject("val_a");
let val2 = inject("val_a2");
</script>

<style scoped></style>
