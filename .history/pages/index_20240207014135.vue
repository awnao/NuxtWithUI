<template>
  <div class="info-container">
    <UAccordion :items="items" :ui="{ wrapper: 'flex flex-col w-full' }">
      <template #default="{ item, index, open }">
        <UButton
          color="gray"
          variant="ghost"
          class="border-b border-gray-200 dark:border-gray-700"
          :ui="{ rounded: 'rounded-none', padding: { sm: 'p-3' } }"
        >
          <template #leading>
            <div
              class="w-6 h-6 rounded-full bg-primary-500 dark:bg-primary-400 flex items-center justify-center -my-1"
            >
              <UIcon :name="item.icon" class="w-4 h-4 text-white dark:text-gray-900" />
            </div>
          </template>

          <span class="truncate">{{ index + 1 }}. {{ item.label }}</span>

          <template #trailing>
            <UIcon
              name="i-heroicons-chevron-right-20-solid"
              class="w-5 h-5 ms-auto transform transition-transform duration-200"
              :class="[open && 'rotate-90']"
            />
          </template>
        </UButton>
      </template>
    </UAccordion>
  </div>

  <div
    class="py-8 px-8 max-w-sm mx-auto bg-white rounded-xl shadow-lg space-y-2 sm:py-4 sm:flex sm:items-center sm:space-y-0 sm:space-x-6"
  >
    <img
      class="block mx-auto h-24 rounded-full sm:mx-0 sm:shrink-0"
      src="http://avatars.steamstatic.com/7a1b2b4cb433e1ec316e3d69592e9b31fc4e261d_full.jpg"
      alt="King"
    />
    <div class="text-center space-y-2 sm:text-left">
      <div class="space-y-0.5">
        <UTooltip text="G.O.A.T">
          <p class="text-lg text-black font-semibold">XxKINGxX</p>
        </UTooltip>
      </div>

      <nuxt-link to="https://steamcommunity.com/id/01000111010011110100000101010100/">
        <button
          class="px-4 py-1 text-sm text-purple-600 font-semibold rounded-full border border-purple-200 hover:text-white hover:bg-purple-600 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-purple-600 focus:ring-offset-2"
        >
          <div class="info-author text-base">
            <UIcon name="i-bi:steam" dynamic /> Steam
          </div>
        </button>
      </nuxt-link>
    </div>
  </div>
</template>

<script setup lang="ts">
const servidorInfo = "Información del servidor...";
const comandos = ["Comando 1", "Comando 2", "Comando 3"];
const nosotrosInfo = "Información sobre nosotros...";
const modoInfo = "Modo de funcionamiento...";
</script>

<style scoped>
@media (prefers-color-scheme: dark) {
  .dark\:text-black {
    --tw-text-opacity: 1;
    color: rgb(0 0 0 / var(--tw-text-opacity));
  }
}

.info-author {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0.2em;
}
.p_v1 {
  flex-shrink: 0;
  font-weight: 700;
  font-size: 1.1rem /* 20px */;
  line-height: 1.75rem /* 28px */;
  --tw-text-opacity: 1;
  color: #555;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.375rem /* 6px */;
}
.info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.info-section {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 80%;
  max-width: 600px;
  transition: transform 0.3s ease;
}

.info-section:hover {
  transform: translateY(-5px);
}

h1 {
  font-size: 1.5em;
  margin-bottom: 10px;
  color: #333;
  display: flex;
  align-items: center;
}

i {
  margin-right: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 5px;
  color: #555;
}
.image-section {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 80%;
  max-width: 600px;
  transition: transform 0.3s ease;
}

.image-section:hover {
  transform: translateY(-5px);
}

.image-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
}

.centered-image {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 5px; /* Ajusta el espacio entre las imágenes según sea necesario */
}

.centered-image img {
  width: 100px; /* Ajusta el tamaño según sea necesario */
  height: auto;
  border-radius: 8px;
}
</style>
