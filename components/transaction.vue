<script setup>
const items = [
  [
    {
      label: 'Edit',
      icon: 'heroicons:pencil-square-16-solid',
      click: () => {
        console.log('edit')
      }
    },
    {
      label: 'Delete',
      icon: 'heroicons:trash-16-solid',
      click: () => {
        console.log('delete')
      }
    }
  ]
]

const { currency } = useCurrency(3000)
</script>
<template>
  <div class="grid grid-cols-2 py-4 border-b border-gray-200 dark:border-gray-800 text-gray-900 dark:text-gray-100">
    <div class="flex items-center justify-between">
      <div class="flex items-center space-x-1">
        <UIcon name="heroicons:arrow-up-right" class="text-green-600"/>
        <div>Salary</div>
      </div>
      <div>
        <UBadge color="white">Category</UBadge>
      </div>
    </div>
    <div class="flex items-center justify-end space-x-2">
      <div>{{ currency  }}</div>
      <div>
        <UDropdown :items="items" :popper="{ arrow: true }">
          <UButton color="white" variant="ghost" trailing-icon="heroicons:ellipsis-horizontal-16-solid" />
        </UDropdown>
      </div>
    </div>
  </div>
</template>