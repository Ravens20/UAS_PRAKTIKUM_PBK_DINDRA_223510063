<template>
  <q-card class="weather-widget">
    <q-card-section>
      <div class="text-h6">Widget Cuaca</div>
      <div class="q-gutter-md">
        <q-input
          v-model="location"
          outlined
          dense
          placeholder="Masukkan lokasi..."
          @keyup.enter="fetchWeatherData"
        />
        <q-btn color="primary" label="Dapatkan Cuaca" @click="fetchWeatherData" class="q-ml-md" />
      </div>
    </q-card-section>

    <q-card-section v-if="weatherData.length">
      <div class="forecast-container">
        <div class="forecast-row" v-for="(row, index) in forecastRows" :key="index">
          <div v-for="forecast in row" :key="forecast.dt" class="forecast-item">
            <div class="forecast-time">{{ formatTime(forecast.dt) }}</div>
            <div class="forecast-icon">
              <img :src="getWeatherIconUrl(forecast.weather[0].icon)" :alt="forecast.weather[0].description" class="weather-icon" />
            </div>
            <div class="forecast-temp">{{ Math.round(forecast.main.temp) }}°C</div>
            <div class="forecast-description">{{ forecastDescription(forecast) }}</div>
          </div>
        </div>
      </div>
    </q-card-section>

    <q-card-section v-else>
      <div class="text-center text-warning" v-if="error">{{ errorMessage }}</div>
      <div class="text-center" v-else>
        <q-spinner-hourglass v-if="loading" size="40px" color="primary" />
        <div v-else>Data cuaca tidak tersedia.</div>
      </div>
    </q-card-section>
  </q-card>
</template>

<script>
import axios from 'axios';

export default {
  name: 'WeatherWidget',
  data() {
    return {
      location: '',
      weatherData: [],
      loading: false,
      error: false
    };
  },
  computed: {
    errorMessage() {
      return 'Gagal mendapatkan data cuaca. Silakan coba lagi nanti.';
    },
    forecastRows() {
      // Split weatherData into two rows, each with 4 items
      const rows = [];
      for (let i = 0; i < this.weatherData.length; i += 4) {
        rows.push(this.weatherData.slice(i, i + 4));
      }
      return rows;
    }
  },
  methods: {
    fetchWeatherData() {
      if (!this.location) {
        return;
      }

      this.loading = true;
      this.error = false;

      const apiKey = 'af6d66eacf9124a1fd6fe773d315152d';
      const apiUrl = 'https://api.openweathermap.org/data/2.5/forecast';

      axios.get(apiUrl, {
        params: {
          q: this.location,
          appid: apiKey,
          units: 'metric'
        }
      })
      .then(response => {
        this.processWeatherData(response.data);
        this.loading = false;
      })
      .catch(error => {
        console.error('Error fetching weather data:', error);
        this.error = true;
        this.loading = false;
      });
    },
    processWeatherData(data) {
      // Filter data untuk mendapatkan ramalan dalam 24 jam ke depan
      const now = new Date();
      const oneDayAhead = new Date(now.getTime() + 24 * 60 * 60 * 1000);

      this.weatherData = data.list.filter(forecast => {
        const forecastDate = new Date(forecast.dt * 1000);
        return forecastDate >= now && forecastDate <= oneDayAhead;
      });
    },
    formatTime(timestamp) {
      const date = new Date(timestamp * 1000);
      return date.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
    },
    getWeatherIconUrl(icon) {
      return `https://openweathermap.org/img/wn/${icon}.png`;
    },
    forecastDescription(forecast) {
      // Deskripsi cuaca dalam bahasa Indonesia untuk semua kondisi
      switch (forecast.weather[0].description) {
        case 'clear sky':
          return 'Langit Cerah';
        case 'few clouds':
          return 'Berawan Sedikit';
        case 'scattered clouds':
          return 'Awan Berkepul-kepul';
        case 'broken clouds':
          return 'Awan Mendung';
        case 'shower rain':
          return 'Hujan Rintik-rintik';
        case 'rain':
          return 'Hujan';
        case 'thunderstorm':
          return 'Badai Petir';
        case 'snow':
          return 'Salju';
        case 'mist':
          return 'Kabut';
        default:
          return forecast.weather[0].description;
      }
    }
  }
};
</script>

<style scoped>
.weather-widget {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 75px;
  z-index: 0;
  background: linear-gradient(to bottom, #3a6186, #89253e); /* Gradient background */
  color: #fff; /* Text color */
  font-family: 'Roboto', sans-serif; /* Font family */
}

.forecast-container {
  display: flex;
  flex-direction: column;
}

.forecast-row {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.forecast-item {
  width: calc(25% - 0.5rem);
  text-align: center;
  padding: 1rem;
  border-radius: 8px;
  background-color: rgba(255, 255, 255, 0.1); /* Background color with transparency */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.forecast-item img.weather-icon {
  max-width: 50px;
  margin-bottom: 10px;
  background-color: #75ddfd;
  border-radius: 10px;
}

.forecast-time {
  font-size: 14px;
  font-weight: bold;
  color: #fff;
  margin-bottom: 5px;
}

.forecast-temp {
  font-size: 18px;
  font-weight: bold;
  color: #fff;
  margin-bottom: 5px;
}

.forecast-description {
  font-size: 14px;
  color: #ddd;
}

.text-warning {
  color: #ffcc00; /* Yellow warning text */
}

.q-input, .q-btn {
  color: #fff; /* Input and button text color */
}

.q-btn {
  background-color: #2980b9; /* Button background color */
}

.q-btn:hover {
  opacity: 0.8;
}
</style>
