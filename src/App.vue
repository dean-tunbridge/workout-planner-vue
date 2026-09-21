<script setup lang="ts">
import Welcome from './components/pages/Welcome.vue'
import Layout from './components/layouts/Layout.vue'
import Dashboard from './components/pages/Dashboard.vue'
import Workout from './components/pages/Workout.vue'
import { computed, onMounted, ref } from 'vue'
import { workoutProgram, type ExerciseData } from './utils/index.ts'

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

const isWorkoutComplete = computed(() => {
  const currentWorkout = data.value?.[currWorkout.value]
  if (!currentWorkout) return false

  const isCompleteCheck = Object.values(currentWorkout).every((ex) => !!ex)
  return isCompleteCheck
})

const firstIncompleteWorkoutIndex = computed(() => {
  const allWorkouts = data.value
  if (!allWorkouts) {
    return -1
  }

  for (const [index, workout] of Object.entries(allWorkouts)) {
    const isComplete = Object.values(workout).every((ex) => !!ex)
    if (!isComplete) {
      return parseInt(index)
    }
  }
  return -1
})

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

function handleResetPlan() {
  currDisplay.value = 2
  currWorkout.value = -1
  data.value = defaultData
  localStorage.removeItem('workouts')
}

onMounted(() => {
  if (!localStorage) return
  if (localStorage.getItem('workouts')) {
    const savedData = JSON.parse(localStorage.getItem('workouts') || 'null')
    data.value = savedData
    currDisplay.value = 2
  }
})
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
      :handleSaveWorkout="handleSaveWorkout"
      :isWorkoutComplete="isWorkoutComplete"
      :data="data"
      :currWorkout="currWorkout"
      v-if="workoutProgram?.[currWorkout]" />
  </Layout>
</template>

<style scoped></style>
