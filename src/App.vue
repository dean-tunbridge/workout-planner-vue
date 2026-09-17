<script setup lang="ts">
import Welcome from './components/pages/Welcome.vue'
import Layout from './components/layouts/Layout.vue'
import Dashboard from './components/pages/Dashboard.vue'
import Workout from './components/pages/Workout.vue'
import { ref } from 'vue'
import { workoutProgram, type ExerciseData } from './utils/index.ts'

const firstIncompleteWorkoutIndex = 0

const handleResetPlan = () => {
  console.log('Reset plan')
}

const defaultData: Record<number, ExerciseData> = {}
for (let workoutIndex in workoutProgram) {
  const workoutData = workoutProgram[workoutIndex]
  defaultData[workoutIndex] = {}

  for (let e of workoutData.workout) {
    defaultData[workoutIndex][e.name] = ''
  }
}

const currDisplay = ref(2)
const data = ref(defaultData)
const currWorkout = ref(-1)

function handleDisplayChange(index: number) {
  currDisplay.value = index
}

function handleSelectWorkout(index: number) {
  currDisplay.value = 3
  currWorkout.value = index
}

function handleSaveWorkout() {
  localStorage.setItem('workouts', JSON.stringify(data.value))
}
</script>

<template>
  <Layout>
    <Welcome />
    <Dashboard
      :handle-select-workout="handleSelectWorkout"
      :first-incomplete-workout-index="firstIncompleteWorkoutIndex"
      :handle-reset-plan="handleResetPlan" />
    <Workout
      :data="data"
      :currWorkout="currWorkout"
      v-if="workoutProgram?.[currWorkout]" />
  </Layout>
</template>

<style scoped></style>
