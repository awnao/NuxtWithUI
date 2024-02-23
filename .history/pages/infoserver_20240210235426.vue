<template>
  <div></div>
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
      const response = await fetch(
        `http://localhost:3004/flow/paymentStatus/40AB7F56FD9F23EDDF96F85F532D6A13E467BF1H`
      );
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
