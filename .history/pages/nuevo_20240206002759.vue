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
          <div class="flex items-center space-x-4">
            <UAvatar
              class="h-12 w-12"
              size="lg"
              src="https://avatars.githubusercontent.com/u/739984?v=4"
              alt="Avatar"
            />
            <div class="space-y-2">
              <p class="h-4 w-[240px]">KingTottyMan</p>
              <p class="h-4 w-[200px]">Diseñador Grafico</p>
            </div>
          </div>
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

<script setup lang="ts">
const links = [
  {
    label: "Home",
    icon: "i-heroicons-home",
    to: "/",
  },
  {
    label: "Navigation",
    icon: "i-heroicons-square-3-stack-3d",
  },
  {
    label: "Breadcrumb",
    icon: "i-heroicons-link",
  },
];
</script>
