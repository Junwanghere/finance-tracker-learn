<template>
  <div>
    <div class="font-bold" :class="[color]">{{ title }}</div>
    <div class="text-2xl font-extrabold text-black dark:text-white mb-2">
      <USkeleton class="h-8 w-full" v-if="loading" />
      <div v-else>
        {{ currency }}
      </div>
    </div>
    <div>
      <USkeleton v-if="loading" class="h-6 w-full" />
      <div v-else class="flex space-x-1 items-center text-sm">
        <UIcon :name="trendingIcon" class="w-6 h-6" :class="{ 'green': trendingUp, 'red': !trendingUp}"/>
        <div class="text-gray-500 dark:text-gray-400">
          {{ trendPercentage }} vs last period
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  title: String,
  loading: Boolean,
  color: String,
  lastAmount: Number,
  amount: Number
})

const { currency } = useCurrency(props.amount)

const trendingUp = computed(() => {
  return props.amount >= props.lastAmount
})

const trendingIconOptions = ['heroicons:arrow-trending-up', 'heroicons:arrow-trending-down']

const trendingIcon = computed(() => {
  return props.amount > props.lastAmount ? trendingIconOptions[0] : trendingIconOptions[1]
})

const trendPercentage = computed(() => {
  if(props.amout == 0 || props.lastAmount == 0) return '%'

  const biggerValue = Math.max(props.amount, props.lastAmount)
  const smallerValue = Math.min(props.amount, props.lastAmount)

  const percentage = Math.ceil((smallerValue/biggerValue)*100)
  return`${percentage}%` 
})
</script>

<style scoped>
.green {
  @apply text-green-600 dark:text-green-400
}

.red {
  @apply text-red-600 dark:text-red-400
}
</style>