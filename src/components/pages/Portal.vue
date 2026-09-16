<script setup lang="ts">
import { Teleport } from 'vue'
</script>
<template>
  <Teleport to="#portal">
    <div class="portal-container">
      <div
        role="button"
        tabindex="0"
        @click="() => {}"
        class="portal-underlay"></div>
    </div>
  </Teleport>
</template>

<style scoped></style>
