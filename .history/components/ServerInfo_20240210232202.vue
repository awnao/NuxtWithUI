<!-- components/ServerInfo.vue -->

<template>
  <div>
    <div v-if="serverInfo">
      <div v-if="serverInfo.hostname === ''" class="circle-red">Servidor Apagado</div>
      <div v-else class="circle-green">Servidor Encendido</div>
      Nombre del Servidor: {{ serverInfo.hostname }} <br />
      Mapa Actual: {{ serverInfo.map }} <br />
      Jugadores: {{ serverInfo.num_players }} / {{ serverInfo.max_players }}
    </div>
    <table v-if="serverInfo">
      <tr>
        <th>#</th>
        <th>Jugadores</th>
        <th>Puntaje</th>
      </tr>
      <tr v-for="(player, index) in serverInfo.players" :key="index">
        <td>{{ player.id }}</td>
        <td>{{ player.name }}</td>
        <td>{{ player.score }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      serverInfo: null,
    };
  },
  async mounted() {
    await this.getServerInfo();
  },
  methods: {
    async getServerInfo() {
      try {
        const response = await this.$axios.get("http://localhost/WEB-COX-CS/");
        this.serverInfo = response.data;
      } catch (error) {
        console.error("Error fetching server info:", error);
      }
    },
  },
};
</script>

<style>
/* Estilos CSS */
</style>
