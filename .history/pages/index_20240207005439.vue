<script setup lang="ts">
const isOpen = ref(false);

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
export default {
  data() {
    return {
      servidorInfo: "Información del servidor...",
      comandos: ["Comando 1", "Comando 2", "Comando 3"],
      nosotrosInfo: "Información sobre nosotros...",
      modoInfo: "Modo de funcionamiento...",
    };
  },
};
</script>
<template>
  <div class="info-container">
    <section class="info-section">
      <h1><UIcon name="i-basil:server-solid" dynamic />Servidor</h1>
      <p class="dark:text-black p_v1">
        {{ servidorInfo }}
      </p>
    </section>

    <section class="info-section">
      <h1><UIcon name="i-clarity:command-solid" dynamic />Comandos</h1>
      <ul>
        <li v-for="comando in comandos" :key="comando">
          <p class="p_v1">
            {{ comando }}
          </p>
        </li>
      </ul>
    </section>

    <section class="info-section">
      <h1><UIcon name="i-fluent:people-community-32-filled" dynamic />Nosotros</h1>
      <p class="dark:text-black p_v1">
        {{ nosotrosInfo }}
      </p>
    </section>

    <section class="info-section">
      <h1><UIcon name="i-ri:function-line" dynamic />Modo</h1>
      <p class="dark:text-black p_v1">
        {{ modoInfo }}
      </p>
    </section>

    <section class="image-section">
      <h1><UIcon name="i-entypo:images" dynamic />Imágenes Adicionales</h1>
      <div class="image-container">
        <div class="centered-image">
          <img
            src="http://cdn.discordapp.com/icons/792159403754127370/35e2e525dc2a52d4ae5edd3c893c1245.webp?size=128"
            alt="Image 1"
          />
        </div>
        <div class="centered-image">
          <img
            src="http://img.freepik.com/foto-gratis/fondo-pantalla-abstracto-nebulosa-ultra-detallado-4_1562-749.jpg?size=626&ext=jpg&ga=GA1.1.1880011253.1705190400&semt=ais"
            alt="Image 2"
          />
        </div>
        <!-- Agrega más imágenes según sea necesario -->
      </div>
    </section>
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
        <p class="text-lg text-black font-semibold">XxKINGxX</p>
        <div class="text-slate-500 font-medium"><UBreadcrumb :links="links" /></div>
      </div>
      <nuxt-link to="https://steamcommunity.com/id/01000111010011110100000101010100/">
        <button
          class="px-4 py-1 text-sm text-purple-600 font-semibold rounded-full border border-purple-200 hover:text-white hover:bg-purple-600 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-purple-600 focus:ring-offset-2"
        >
          Steam
        </button>
      </nuxt-link>
    </div>
  </div>
</template>

<style scoped>
@media (prefers-color-scheme: dark) {
  .dark\:text-black {
    --tw-text-opacity: 1;
    color: rgb(0 0 0 / var(--tw-text-opacity));
  }
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
