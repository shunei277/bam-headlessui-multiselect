<template>
  <label><input
    v-model="canSupportJapanese"
    type="checkbox"
  >日本語</label>
  <div class="flex justify-center px-4">
    <component :is="Multiselect" />
  </div>
</template>

<script lang="ts" setup>
import { computed, ref } from 'vue';
import MultiselectSample from '@/components/MultiselectSample.vue';
import MultiselectWithJapanese from '@/components/MultiselectSupportingJapanese.vue';

const canSupportJapanese = ref(false);
const Multiselect = computed(() => (
  canSupportJapanese.value ? MultiselectWithJapanese : MultiselectSample));
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
