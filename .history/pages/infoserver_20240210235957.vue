<template>
  <div>
    {{ serverInfo.gq_type }}
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
