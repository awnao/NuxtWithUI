<template>
  <UContainer>
    <UCard class="mt-10">
      <template #header>
        <div class="flex justify-between">
          <h1
            v-if="$colorMode.preference === 'dark'"
            class="flex-shrink-0 font-bold text-xl text-gray-900 dark:text-white flex items-end gap-1.5"
          >
            Soccerjam -- Chile<UBadge color="primary" variant="soft">SJ.PLUS [v1]</UBadge>
          </h1>
          <h1
            v-if="$colorMode.preference === 'light'"
            class="flex-shrink-0 font-bold text-xl text-gray-900 dark:text-white flex items-end gap-1.5"
          >
            Soccerjam -- Chile<UBadge color="purple" variant="soft">SJ.PLUS [v1]</UBadge>
          </h1>
          <h1
            v-if="$colorMode.preference === 'system'"
            class="flex-shrink-0 font-bold text-xl text-gray-900 dark:text-white flex items-end gap-1.5"
          >
            Soccerjam -- Chile<UBadge color="sky" variant="soft">SJ.PLUS [v1]</UBadge>
          </h1>
          <ClientOnly>
            <UButton
              :icon="isDark ? 'i-heroicons-moon-20-solid' : 'i-heroicons-sun-20-solid'"
              color="gray"
              variant="ghost"
              aria-label="Theme"
              @click="isDark = !isDark"
            />
            <template #fallback>
              <div class="w-8 h-8" />
            </template>
          </ClientOnly>
        </div>
      </template>

      <slot />
    </UCard>
  </UContainer>
</template>

<script setup>
const colorMode = useColorMode();
const isDark = computed({
  get() {
    return colorMode.value === "dark";
  },
  set() {
    colorMode.preference = colorMode.value === "dark" ? "light" : "dark";
  },
});
</script>
