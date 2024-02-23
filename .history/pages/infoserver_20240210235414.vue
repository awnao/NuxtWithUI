<template>
  <div></div>
</template>

<script>
const response = await fetch("http://localhost:3004/flow/createPayment", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ monto: this.monto }),
});
</script>
