<script setup lang="ts">
import { gymHealthFacts } from '../../utils'
import Grid from './Grid.vue'

interface Props {
  handleSelectWorkout: (index: number) => void
  handleResetPlan: () => void
  firstIncompleteWorkoutIndex: number
}

const props = defineProps<Props>()

const randomNumber = Math.floor(Math.random() * gymHealthFacts.length)
const todaysFact = gymHealthFacts[randomNumber]
</script>

<template>
  <section id="dashboard">
    <div class="card tip-container">
      <h2>Welcome</h2>
      <div>
        <p class="tip"><strong>Daily Tip</strong><br />{{ todaysFact }}</p>
      </div>
      <button
        @click="
          () =>
            handleSelectWorkout(
              firstIncompleteWorkoutIndex < 0 ? 0 : firstIncompleteWorkoutIndex,
            )
        ">
        Start workout &rarr;
      </button>
    </div>
    <Grid v-bind="props" />
  </section>
</template>

<style scoped>
.tip-container,
.tip-container div,
#dashboard {
  display: flex;
  align-items: center;
}

.tip-container,
#dashboard {
  flex-direction: column;
}

#dashboard {
  gap: 2rem;
}

.tip-container {
  gap: 0.5rem;
}

@media (min-width: 640px) {
  .tip-container {
    gap: 1rem;
  }
}
</style>
