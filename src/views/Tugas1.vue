<template>
    <div class="custom-page">
      <div class="custom-container">
        <div class="custom-card">
          <div class="custom-card-header">
            <h2 class="custom-card-title">Tugas 1</h2>
          </div>
          <div class="custom-card-content">
            <p class="custom-card-description">Tidak Ada.</p>
          </div>
          <div class="custom-card-footer">
            <button @click="goHome" class="home-button">Kembali ke Beranda</button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'App',
    methods: {
      goHome() {
        // Logika untuk kembali ke halaman beranda
        // Misalnya, menggunakan router:
        this.$router.push('/');
      }
    }
  };
  </script>
  
  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');
  
  .custom-page {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background: linear-gradient(135deg, #1d2b64, #f8cdda);
    padding: 0;
    font-family: 'Poppins', sans-serif;
  }
  
  .custom-container {
    max-width: 400px;
    width: 100%;
    padding: 2rem;
  }
  
  .custom-card {
    background-color: #fff;
    border-radius: 16px;
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
    overflow: hidden;
    transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  
  .custom-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  }
  
  .custom-card-header {
    background: linear-gradient(135deg, #6e45e2, #88d3ce);
    padding: 1rem;
    text-align: center;
  }
  
  .custom-card-title {
    font-size: 2rem;
    font-weight: 600;
    color: #fff;
    margin: 0;
  }
  
  .custom-card-content {
    padding: 2rem;
    text-align: center;
  }
  
  .custom-card-description {
    font-size: 1.2rem;
    color: #333;
    margin-bottom: 1.5rem;
  }
  
  .custom-card-footer {
    padding: 1rem;
    text-align: center;
  }
  
  .home-button {
    background-color: #6e45e2;
    color: #fff;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .home-button:hover {
    background-color: #88d3ce;
  }
  </style>
  