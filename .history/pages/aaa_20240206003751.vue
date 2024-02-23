<template>
  <div>
    <script src="https://cdn.lordicon.com/lordicon.js"></script>
    <lord-icon
      :src="iconSrc"
      trigger="hover"
      style="width: 250px; height: 250px"
    ></lord-icon>
  </div>
</template>

<script>
export default {
  data() {
    return {
      iconSrc: "https://cdn.lordicon.com/uwinmnkh.json",
    };
  },
};
</script>
