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

const currDisplay = ref(1)
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

  currDisplay.value = 2
  currWorkout.value = -1
}
</script>

<template>
  <Layout>
    <Welcome
      :handleDisplayChange="handleDisplayChange"
      v-if="currDisplay == 1" />
    <Dashboard
      v-if="currDisplay == 2"
      :handleSelectWorkout="handleSelectWorkout"
      :firstIncompleteWorkoutIndex="firstIncompleteWorkoutIndex"
      :handleResetPlan="handleResetPlan" />
    <Workout
      :data="data"
      :currWorkout="currWorkout"
      v-if="workoutProgram?.[currWorkout]" />
  </Layout>
</template>

<style scoped></style>
