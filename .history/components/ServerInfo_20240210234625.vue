<template>
  <div>
    <div v-if="serverInfo">
      <p>Servidor Encendido</p>
      <p v-else>Servidor Apagado</p>
      <p>Nombre del Servidor: {{ serverInfo["38.7.218.60:27021"].gq_hostname }}</p>
      <p>Mapa Actual: {{ serverInfo["38.7.218.60:27021"].gq_mapname }}</p>
      <p>
        Jugadores: {{ serverInfo["38.7.218.60:27021"].gq_numplayers }} /
        {{ serverInfo["38.7.218.60:27021"].gq_maxplayers }}
      </p>
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Jugadores</th>
            <th>Puntaje</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(player, index) in serverInfo['38.7.218.60:27021'].players"
            :key="index"
          >
            <td>{{ player.id }}</td>
            <td>{{ player.name }}</td>
            <td>{{ player.score }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-else>
      <p>Error al cargar la información del servidor.</p>
    </div>
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
      const data = await response.json();
      this.serverInfo = data;
    } catch (error) {
      console.error("Error fetching server info:", error);
    }
  },
};
</script>
