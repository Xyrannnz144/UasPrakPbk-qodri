<template>
    <div class="weather-container">
      <div class="search-bar">
        <input
          type="text"
          v-model="city"
          placeholder="Masukkan Nama Kota"
          @keyup.enter="fetchWeather"
          class="city-input"
        />
        <button @click="fetchWeather" class="search-button">Cari</button>
      </div>
      <div v-if="weather.main" class="weather-info bg-gradient-green rounded-borders shadow-2">
        <h2 class="city-name">{{ city }}</h2>
        <div class="weather-icon" :class="'icon-' + weather.main.toLowerCase()">
          <span v-if="weather.main === 'Clear'">☀️</span>
          <span v-else-if="weather.main === 'Clouds'">☁️</span>
          <span v-else-if="weather.main === 'Rain'">🌧️</span>
          <span v-else-if="weather.main === 'Snow'">❄️</span>
          <span v-else-if="weather.main === 'Thunderstorm'">🌩️</span>
          <span v-else-if="weather.main === 'Drizzle'">🌦️</span>
          <span v-else>🌥️</span>
        </div>
        <div class="description">{{ weatherDescription }}</div>
        <div class="temperature">{{ temperature }}°C</div>
      </div>
      <div v-else class="no-data rounded-borders shadow-2">Data cuaca tidak tersedia.</div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        city: 'Jakarta',
        weather: {},
        temperature: null,
      };
    },
    computed: {
      weatherDescription() {
        return this.weather.description
          ? this.weather.description.charAt(0).toUpperCase() + this.weather.description.slice(1)
          : '';
      },
    },
    methods: {
      async fetchWeather() {
        if (!this.city) return;
        const API_KEY = '4d1db2666da951482ad444c5f52dc755';
        try {
          const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${API_KEY}&units=metric`);
          this.weather = response.data.weather[0];
          this.temperature = response.data.main.temp;
        } catch (error) {
          console.error("Error fetching weather data:", error);
          alert("Kota tidak ditemukan atau terjadi kesalahan jaringan.");
        }
      },
    },
    mounted() {
      this.fetchWeather();
    },
  };
  </script>
  
  <style scoped>
  /* General Styles */
  .weather-container {
    max-width: 600px;
    margin: 50px auto;
    padding: 30px;
    background-color: #64b5f6; /* Warna biru cerah */
    border-radius: 16px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2); /* Efek bayangan yang lebih kuat */
    font-family: 'Arial', sans-serif;
    text-align: center;
    color: #fff; /* Warna teks putih */
  }
  
  .search-bar {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  .city-input {
    padding: 12px;
    border: 1px solid #ccc;
    border-radius: 10px 0 0 10px;
    width: 70%;
    font-size: 18px;
    outline: none;
  }
  
  .search-button {
    padding: 12px 20px;
    border: none;
    border-radius: 0 10px 10px 0;
    background-color: #1e88e5; /* Warna biru lebih gelap */
    color: #fff;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .search-button:hover {
    background-color: #1565c0; /* Warna biru muda saat dihover */
  }
  
  .weather-info {
    padding: 25px;
    border-radius: 16px;
    margin-top: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Bayangan yang lebih lembut */
  }
  
  .weather-icon {
    font-size: 80px;
    margin: 20px 0;
  }
  
  .icon-sunny {
    animation: spin 5s linear infinite;
  }
  
  .icon-cloudy {
    animation: drift 4s ease-in-out infinite;
  }
  
  .icon-rainy {
    animation: rain 1s linear infinite;
  }
  
  .icon-snowy {
    animation: snow 1.5s linear infinite;
  }
  
  .icon-thunderstorm {
    animation: flash 0.6s linear infinite;
  }
  
  .icon-drizzle {
    animation: drizzle 1.2s linear infinite;
  }
  
  
  .description {
    font-size: 20px;
    margin: 10px 0;
  }
  
  .temperature {
    font-size: 28px;
    font-weight: bold;
  }
  
  .no-data {
    font-size: 22px;
    margin-top: 30px;
  }
  
  .bg-gradient-green {
    background: linear-gradient(to bottom, #43a047, #66bb6a); /* Gradien hijau */
    color: #2c3e50; /* Warna teks lebih gelap */
  }
  
  @keyframes spin {
    to {
      transform: rotate(360deg);
    }
  }
  
  @keyframes drift {
    0%, 100% {
      transform: translateX(0);
    }
    50% {
      transform: translateX(10px);
    }
  }
  
  @keyframes rain {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(10px);
    }
  }
  
  @keyframes snow {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(5px);
    }
  }
  
  @keyframes flash {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0.5;
    }
  }
  
  @keyframes drizzle {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(7px);
    }
  }
  </style>
  