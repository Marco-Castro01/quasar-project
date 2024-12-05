<template>
  <div class="main-container">
    <div class="background-animation">
      <div class="rhombus" v-for="n in 10" :key="n"></div>
    </div>
    <h1 class="main-title">Búsqueda con Axios</h1>

    <div class="input-container">
      <q-input v-model="text" label="Ingresa tu búsqueda" class="custom-input" />
      <q-btn @click="obtenerDatos" label="Buscar" class="custom-btn" />
    </div>

    <div v-if="resultado" class="results-container">
      <h2 class="results-title">Resultados</h2>
      <div class="card-container">
        <div class="card" v-for="photo in resultado.photos" :key="photo.id">
          <img :src="photo.src.medium" :alt="photo.alt" class="card-img" />
        </div>
      </div>
    </div>

    <div v-if="error" class="error-container">
      <p>Error al obtener datos: {{ error }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      text: '',
      resultado: null,
      error: null
    };
  },
  methods: {
    async obtenerDatos() {
      this.error = null;
      try {
        const response = await axios.get(`https://api.pexels.com/v1/search?query=${this.text}`, {
          headers: {
            Authorization: 'E72kNwJNKTZFbCQctvkpnDZesBH1VcGCh1obkwVn9fIz18SyUUJOWytb'
          }
        });
        this.resultado = response.data;
      } catch (error) {
        console.error('Error al obtener datos:', error);
        this.error = 'Error al obtener datos';
        this.resultado = null;
      }
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');

body, html {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: auto;
}

.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40px;
  background: linear-gradient(135deg, #f0f8ff, #e0ffff);
  font-family: 'Poppins', sans-serif;
  position: relative;
  overflow: visible;
}

.background-animation {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  pointer-events: none;
  z-index: 0;
}

.rhombus {
  position: absolute;
  background: rgba(0, 123, 255, 0.3);
  width: 30px;
  height: 30px;
  transform: rotate(45deg);
  animation: fall 5s linear infinite;
}

.rhombus:nth-child(1) {
  animation-delay: 0s;
  left: 10%;
}

.rhombus:nth-child(2) {
  animation-delay: 1s;
  left: 30%;
}

.rhombus:nth-child(3) {
  animation-delay: 2s;
  left: 50%;
}

.rhombus:nth-child(4) {
  animation-delay: 3s;
  left: 70%;
}

.rhombus:nth-child(5) {
  animation-delay: 4s;
  left: 90%;
}

.rhombus:nth-child(6) {
  animation-delay: 0.5s;
  left: 20%;
}

.rhombus:nth-child(7) {
  animation-delay: 1.5s;
  left: 40%;
}

.rhombus:nth-child(8) {
  animation-delay: 2.5s;
  left: 60%;
}

.rhombus:nth-child(9) {
  animation-delay: 3.5s;
  left: 80%;
}

.rhombus:nth-child(10) {
  animation-delay: 4.5s;
  left: 100%;
}

@keyframes fall {
  0% {
    transform: translateY(-100px) rotate(45deg);
    opacity: 0;
  }
  50% {
    opacity: 0.3;
  }
  100% {
    transform: translateY(100vh) rotate(45deg);
    opacity: 0;
  }
}

.main-title {
  font-size: 3rem;
  color: #333;
  margin-bottom: 30px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
  z-index: 1;
}

.input-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
  margin-bottom: 30px;
  z-index: 1;
}

.custom-input {
  width: 350px;
  border: 2px solid #007bff;
  border-radius: 10px;
  padding: 15px;
  font-size: 1.2rem;
  transition: border-color 0.3s, box-shadow 0.3s;
  z-index: 1;
}

.custom-input:focus {
  border-color: #0056b3;
  box-shadow: 0 0 10px rgba(0, 123, 255, 0.5);
}

.custom-btn {
  width: 180px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 10px;
  padding: 15px;
  font-size: 1.2rem;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
  z-index: 1;
}

.custom-btn:hover {
  background-color: #0056b3;
  box-shadow: 0 0 10px rgba(0, 123, 255, 0.5);
}

.results-container {
  width: 100%;
  max-width: 900px;
  z-index: 1;
}

.results-title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.card {
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s, box-shadow 0.3s;
  width: 200px;
  height: 200px;
  position: relative;
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
}

.card-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 15px;
}

.error-container {
  color: red;
  margin-top: 30px;
  font-size: 1.3rem;
  z-index: 1;
}
</style>
