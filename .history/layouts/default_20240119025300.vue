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
          <ColorScheme
            ><USelect
              v-model="$colorMode.preference"
              :options="['system', 'light', 'dark']"
          /></ColorScheme>
        </div>
      </template>

      <slot />
    </UCard>
  </UContainer>
</template>
