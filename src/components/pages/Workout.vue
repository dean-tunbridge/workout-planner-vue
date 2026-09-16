<script setup lang="ts">
import { workoutProgram } from '../../utils'

const currWorkout = 4

const { workout, warmup } = workoutProgram[currWorkout]
</script>

<template>
  <section id="workout-card">
    <div class="plan-card card">
      <div class="plan-card header">
        <p>Day {{ currWorkout < 9 ? '0' + currWorkout : currWorkout }}</p>
        <i class="fa-solid fa-dumbbell"></i>
      </div>
      <h2>{{ 'push' }} Workout</h2>
    </div>
    <div class="workout-grid">
      <h4 class="grid-name">warmup</h4>
      <h6>Sets</h6>
      <h6>Reps</h6>
      <h6 class="grid-weight">Weight</h6>
      <div
        class="workout-grid-row"
        v-for="(warmups, warmupIndex) in warmup"
        :key="warmupIndex">
        <div class="grid-name">
          <p>{{ warmups.name }}</p>
          <button>
            <i class="fa-regular fa-circle-question"></i>
          </button>
          <p>{{ warmups.sets }}</p>
          <p>{{ warmups.reps }}</p>
          <input class="grid-weights" placeholder="14kg" type="text" disabled />
        </div>
        <div class="workout-grid-line"></div>
        <div
          class="workout-grid-row"
          v-for="(workouts, workoutIndex) in warmup"
          :key="workoutIndex">
          <div class="grid-name">
            <p>{{ workouts.name }}</p>
            <button>
              <i class="fa-regular fa-circle-question"></i>
            </button>
            <p>{{ workouts.sets }}</p>
            <p>{{ workouts.reps }}</p>
            <input class="grid-weights" placeholder="14kg" type="text" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
