<script setup lang="ts">
const isOpen = ref(false);
</script>

<template>
  <div>
    <UButton label="Open" @click="isOpen = true" />

    <USlideover v-model="isOpen">
      <UCard
        class="flex flex-col flex-1"
        :ui="{
          body: { base: 'flex-1' },
          ring: '',
          divide: 'divide-y divide-gray-100 dark:divide-gray-800',
        }"
      >
        <template #header>
          <Placeholder class="h-8" />
          <template>
            <div class="flex items-center space-x-4">
              <USkeleton class="h-12 w-12" :ui="{ rounded: 'rounded-full' }" />
              <div class="space-y-2">
                <USkeleton class="h-4 w-[250px]" />
                <USkeleton class="h-4 w-[200px]" />
              </div>
            </div>
          </template>
        </template>

        <Placeholder class="h-full" />
        hola

        <template #footer>
          king
          <Placeholder class="h-8" />
        </template>
      </UCard>
    </USlideover>
  </div>
</template>
