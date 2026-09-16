<script setup lang="ts">
import Welcome from './components/pages/Welcome.vue'
import Layout from './components/layouts/Layout.vue'
import Dashboard from './components/pages/Dashboard.vue'
import Workout from './components/pages/Workout.vue'

const handleSelectWorkout = (index: number) => {
  console.log('Selected workout:', index)
}

const firstIncompleteWorkoutIndex = 0

const handleResetPlan = (event: PointerEvent) => {
  console.log('Reset plan')
}

const currDisplay = 1
</script>

<template>
  <Layout>
    <Welcome />
    <Dashboard
      :handle-select-workout="handleSelectWorkout"
      :first-incomplete-workout-index="firstIncompleteWorkoutIndex"
      :handle-reset-plan="handleResetPlan" />
    <Workout v-if="currDisplay == 1" />
  </Layout>
</template>

<style scoped></style>
