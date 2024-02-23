<template>
  <div class="flex justify-center">
    <div>
      {{ data["38.7.218.60:27021"].gq_hostname }}
    </div>
  </div>
</template>

<script>
export default {
  async mounted() {
    try {
      const response = await fetch("http://localhost/WEB-COX-CS/");
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      const data = await response.json();
    } catch (error) {
      console.error("Error fetching server info:", error);
    }
  },
};
</script>
