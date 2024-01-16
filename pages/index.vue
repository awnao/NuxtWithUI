<template>
  <div class="info-container">
    <section class="info-section">
      <h1><i class="fas fa-server"></i> Servidor</h1>
      <p>{{ servidorInfo }}</p>
    </section>

    <section class="info-section">
      <h1><i class="fas fa-terminal"></i> Comandos</h1>
      <ul>
        <li v-for="comando in comandos" :key="comando">
          <i class="fas fa-caret-right"></i> {{ comando }}
        </li>
      </ul>
    </section>

    <section class="info-section">
      <h1><UIcon name="i-vscode-icons:default-folder" dynamic /> Nosotros</h1>
      <p>{{ nosotrosInfo }}</p>
    </section>

    <section class="info-section">
      <h1><i class="fas fa-cogs"></i> Modo</h1>
      <p>{{ modoInfo }}</p>
    </section>

    <section class="image-section">
      <h1>Imágenes Adicionales</h1>
      <div class="image-container">
        <div class="centered-image">
          <img
            src="https://img.freepik.com/foto-gratis/leon-melena-arcoiris-ojos-azules_1340-39421.jpg"
            alt="Image 1"
          />
        </div>
        <div class="centered-image">
          <img
            src="https://img.freepik.com/foto-gratis/fondo-pantalla-abstracto-nebulosa-ultra-detallado-4_1562-749.jpg?size=626&ext=jpg&ga=GA1.1.1880011253.1705190400&semt=ais"
            alt="Image 2"
          />
        </div>
        <!-- Agrega más imágenes según sea necesario -->
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      servidorInfo: "Información del servidor...",
      comandos: ["Comando 1", "Comando 2", "Comando 3"],
      nosotrosInfo: "Información sobre nosotros...",
      modoInfo: "Modo de funcionamiento...",
    };
  },
};
</script>

<style scoped>
.info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.info-section {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 80%;
  max-width: 600px;
  transition: transform 0.3s ease;
}

.info-section:hover {
  transform: translateY(-5px);
}

h1 {
  font-size: 1.5em;
  margin-bottom: 10px;
  color: #333;
  display: flex;
  align-items: center;
}

i {
  margin-right: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 5px;
  color: #555;
}
.image-section {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 80%;
  max-width: 600px;
  transition: transform 0.3s ease;
}

.image-section:hover {
  transform: translateY(-5px);
}

.image-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
}

.centered-image {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 5px; /* Ajusta el espacio entre las imágenes según sea necesario */
}

.centered-image img {
  width: 100px; /* Ajusta el tamaño según sea necesario */
  height: auto;
  border-radius: 8px;
}
</style>
