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
      loading: true,
      result: null,
      error: null,
    };
  },
  async created() {
    const token = this.$route.params.token;
    try {
      const response = await fetch("http://localhost:3004/flow/createPayment", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ monto: this.monto }),
      });
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
