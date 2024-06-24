<template>
    <q-page class="weather-page">
      <q-header elevated class="bg-purple">
        <q-toolbar class="toolbar">
          <q-toolbar-title class="title text-white">DETEKSI CUACA</q-toolbar-title>
          <q-space />
          <q-btn-dropdown flat label="TUGAS QODRI" no-caps class="task-dropdown">
            <q-list>
              <q-item clickable v-ripple to="/Tugas1">
                <q-item-section>
                  <q-item-label>Tugas 1</q-item-label>
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple to="/Tugas2">
                <q-item-section>
                  <q-item-label>Tugas 2</q-item-label>
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple to="/Tugas3">
                <q-item-section>
                  <q-item-label>Tugas 3</q-item-label>
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple to="/Tugas4">
                <q-item-section>
                  <q-item-label>Tugas 4</q-item-label>
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple to="/Tugas5">
                <q-item-section>
                  <q-item-label>Tugas 5</q-item-label>
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple to="/Tugas6">
                <q-item-section>
                  <q-item-label>Tugas 6</q-item-label>
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple to="/Tugas7">
                <q-item-section>
                  <q-item-label>Tugas 7</q-item-label>
                </q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
        </q-toolbar>
      </q-header>
  
      <q-card class="weather-card rounded-borders shadow-2">
        <q-card-section class="q-pa-md">
          <h2 class="card-title text-center">INFO CUACA TERKINI</h2>
          <div class="search-bar q-mb-md">
            <q-input v-model="city" placeholder="Masukkan Nama Kota" @keyup.enter="fetchWeather" filled rounded dense />
            <q-btn @click="fetchWeather" label="Cari" color="primary" rounded dense />
          </div>
          <div v-if="weather.main" class="weather-info q-pa-md rounded-borders shadow-2">
            <h2 class="city-name text-center">{{ city }}</h2>
            <q-icon :name="weatherIcon" class="weather-icon q-mb-md" />
            <div class="description text-center">{{ weatherDescription }}</div>
            <div class="temperature text-center">{{ temperature }}°C</div>
          </div>
          <div v-else class="no-data q-pa-md rounded-borders shadow-2 text-center">Data cuaca tidak tersedia.</div>
        </q-card-section>
      </q-card>
    </q-page>
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
      weatherIcon() {
        switch (this.weather.main) {
          case 'Clear':
            return 'mdi-weather-sunny';
          case 'Clouds':
            return 'mdi-weather-cloudy';
          case 'Rain':
            return 'mdi-weather-rainy';
          case 'Snow':
            return 'mdi-weather-snowy';
          case 'Thunderstorm':
            return 'mdi-weather-lightning';
          case 'Drizzle':
            return 'mdi-weather-partly-rainy';
          default:
            return 'mdi-weather-partly-cloudy';
        }
      },
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
  .weather-page {
    background: linear-gradient(to right, #74ebd5, #acb6e5);
    color: #333;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .toolbar {
    background: #5f27cd;
  }
  
  .title {
    font-size: 2em;
    font-weight: bold;
    color: #fff;
  }
  
  .task-dropdown .q-list {
    background-color: #5f27cd;
    color: #fff;
  }
  
  .task-dropdown .q-item {
    padding: 12px;
    border-bottom: 1px solid #5f27cd;
  }
  
  .task-dropdown .q-item:hover {
    background-color: #341f97;
  }
  
  .task-dropdown .q-item-label {
    font-size: 1.2em;
    font-weight: bold;
    color: #fff;
  }
  
  .weather-card {
    background: #fff;
    border-radius: 16px;
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
    width: 90%;
    max-width: 700px;
    margin-top: 40px;
  }
  
  .card-title {
    font-size: 1.8em;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  .search-bar {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  .city-input {
    width: 70%;
    margin-right: 10px;
  }
  
  .search-button {
    background-color: #5f27cd;
  }
  
  .weather-info {
    background: #f6f6f6;
    padding: 20px;
    border-radius: 16px;
    color: #333;
    text-align: center;
  }
  
  .city-name {
    font-size: 1.6em;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
  .weather-icon {
    font-size: 4em;
    color: #5f27cd;
    margin: 20px 0;
  }
  
  .description {
    font-size: 1.2em;
    margin: 10px 0;
  }
  
  .temperature {
    font-size: 2em;
    font-weight: bold;
  }
  
  .no-data {
    font-size: 1.2em;
    color: #999;
    margin-top: 30px;
  }
  </style>
  