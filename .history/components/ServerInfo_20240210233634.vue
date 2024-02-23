<template>
  <div>
    <div v-if="serverInfo">
      <div v-if="serverInfo.hostname === ''" class="circle-red"></div>
      <div v-else class="circle-green"></div>
      <p v-if="serverInfo.hostname === ''" class="text-red">Servidor Apagado</p>
      <p v-else class="text-green">Servidor Encendido</p>
      <p>Nombre del Servidor: {{ serverInfo.hostname }}</p>
      <p>Mapa Actual: {{ serverInfo.map }}</p>
      <p>Jugadores: {{ serverInfo.num_players }} / {{ serverInfo.max_players }}</p>
    </div>
    <table v-if="serverInfo">
      <thead>
        <tr>
          <th>#</th>
          <th>Jugadores</th>
          <th>Puntaje</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(player, index) in serverInfo.players" :key="index">
          <td>{{ player.id }}</td>
          <td>{{ player.name }}</td>
          <td>{{ player.score }}</td>
        </tr>
      </tbody>
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
    try {
      const response = await fetch("http://localhost/WEB-COX-CS/");
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }

      let data;
      const contentType = response.headers.get("content-type");
      if (contentType && contentType.includes("application/json")) {
        data = await response.json();
      } else {
        const text = await response.text();
        console.log("Response is not JSON. Response body:", text);
        // Handle the response as needed, for example, parse the text manually.
      }

      this.serverInfo = data;
    } catch (error) {
      console.error("Error fetching server info:", error);
    }
  },
};
</script>

<style scoped>
.circle-red {
  width: 20px;
  height: 20px;
  background-color: red;
  border-radius: 50%;
  display: inline-block;
}
.circle-green {
  width: 20px;
  height: 20px;
  background-color: green;
  border-radius: 50%;
  display: inline-block;
}
.text-red {
  color: red;
}
.text-green {
  color: green;
}
</style>
