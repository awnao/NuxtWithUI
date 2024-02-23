<template>
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
