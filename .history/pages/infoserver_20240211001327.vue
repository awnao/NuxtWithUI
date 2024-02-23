<template>
  <div class="flex justify-center">
    <div>
      <p>
        {{ serverHostname }}
      </p>
      <p>
        {{ serverJugadores }}
      </p>
      <p>
        {{ serverMapname }}
      </p>

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

<script>
export default {
  data() {
    return {
      serverHostname: null,
      serverJugadores: null,
      serverMapname: null,
    };
  },
  async mounted() {
    try {
      const response = await fetch("http://localhost/WEB-COX-CS/");
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      const data = await response.json();
      // Accede directamente al campo gq_hostname y asígnalo a serverHostname
      this.serverHostname = data["38.7.218.60:27021"].gq_hostname;
      this.serverJugadores = data["38.7.218.60:27021"].gq_numplayers;
      this.serverMapname = data["38.7.218.60:27021"].map;
    } catch (error) {
      console.error("Error fetching server info:", error);
    }
  },
};
</script>
