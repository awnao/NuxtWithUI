<template>
  <div class="">
    {{ serverHostname }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      serverHostname: null,
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
    } catch (error) {
      console.error("Error fetching server info:", error);
    }
  },
};
</script>
