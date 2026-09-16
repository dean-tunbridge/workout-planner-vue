<script setup lang="ts">
import Welcome from './components/pages/Welcome.vue'
import Layout from './components/layouts/Layout.vue'
import Dashboard from './components/pages/Dashboard.vue'
import Workout from './components/pages/Workout.vue'

const currDisplay = 1
</script>

<template>
  <Layout>
    <Welcome v-if="currDisplay == 0" />
    <Dashboard v-if="currDisplay == 1" />
    <Workout v-if="currDisplay == 2" />
  </Layout>
</template>

<style scoped></style>
