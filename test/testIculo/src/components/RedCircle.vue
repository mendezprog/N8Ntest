<template lang="pug">
.circle(:style="{ transform: 'scale(' + scale + ')' }")
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

const scale = ref(1);

onMounted(() => {
  let growing = true;

  setInterval(() => {
    if (growing) {
      scale.value += 0.01;
      if (scale.value > 1.5) {
        growing = false;
      }
    } else {
      scale.value -= 0.01;
      if (scale.value < 1) {
        growing = true;
      }
    }
  }, 16);
});
</script>

<style scoped lang="scss">
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background-color: red;
  transition: transform 0.1s ease-in-out;
}
</style>