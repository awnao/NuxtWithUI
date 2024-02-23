<template>
  <div>
    <h3>Completado</h3>
    <p>Verificando estado del pago...</p>

    <div v-if="loading">
      <p>Obteniendo información del estado del pago...</p>
    </div>

    <div v-if="result && result.status === 'completed'">
      <h4>Resultado del pago:</h4>
      <p>El pago ha sido completado con éxito.</p>
      <pre>{{ result.data | prettyPrint }}</pre>
    </div>

    <div v-if="result && result.status === 'rejected'">
      <h4>Resultado del pago:</h4>
      <p>El pago ha sido rechazado.</p>
      <pre>{{ result.data | prettyPrint }}</pre>
    </div>

    <div v-if="error">
      <h4>Error:</h4>
      <p>Hubo un error al verificar el estado del pago.</p>
      <pre>{{ error }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: true,
      result: null,
      error: null,
    };
  },
  async created() {
    const token = this.$route.params.token;
    try {
      const response = await fetch(`http://localhost/WEB-COX-CS/`);
      const data = await response.json();
      this.result = {
        status: data.status,
        data: data.data,
      };
    } catch (error) {
      console.error("Error al obtener el estado del pago:", error);
      this.error = "Error al obtener el estado del pago";
    } finally {
      this.loading = false;
    }
  },
  filters: {
    prettyPrint(jsonString) {
      try {
        const data = JSON.parse(jsonString);
        return JSON.stringify(data, null, 2);
      } catch (error) {
        console.error("Error al parsear el JSON:", error);
        return jsonString;
      }
    },
  },
};
</script>
