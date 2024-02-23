<template>
  <div>
    <h3>Completado</h3>
    <p>Verificando estado del pago...</p>

    <div v-if="loading">
      <p>Obteniendo información del estado del pago...</p>
    </div>

    {{ data }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      serverInfo: null
    };
  },
  async mounted() {
    try {
      const response = await fetch('http://localhost/server-info.php');
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      const data = await response.json();
      this.serverInfo = data;
    } catch (error) {
      console.error('Error fetching server info:', error);
    }
  }
};
</script>
