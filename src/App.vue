<template>
  <div id="app">
    <Navbar @toggle-sidebar="toggleSidebar" />
    <div class="container">
      <Sidebar :isHidden="isSidebarHidden" />
      <div class="content">
        <router-view />
        <WeatherWidget v-if="selectedTask === 'task1'" />
      </div>
    </div>
    <footer class="footer">
      <p>&copy; 2024 Dindra Desvantio. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'; // Sesuaikan path jika perlu
import Sidebar from './components/Sidebar.vue'; // Sesuaikan path jika perlu

export default {
  name: 'App',

  components: {
    Navbar,
    Sidebar,
  },

  data() {
    return {
      isSidebarHidden: true,
      selectedTask: null
    };
  },

  methods: {
    toggleSidebar() {
      this.isSidebarHidden = !this.isSidebarHidden;
    }
  }
};
</script>

<style scoped>
/* Reset margin dan padding pada elemen bawaan */
body,
html {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden; /* Menghilangkan scroll baik horizontal maupun vertical */
}

/* CSS untuk container utama */
.container {
  width: 100%; /* Memastikan container utama mengambil lebar 100% dari layar */
  height: 100%; /* Memastikan container utama mengambil tinggi 100% dari layar */
  display: flex;
  flex-direction: column;
}

/* CSS untuk footer */
.footer {
  background: linear-gradient(to bottom, #3a6186, #89253e); /* Gradien yang sama dengan sidebar */
  color: #fff;
  text-align: center;
  padding: 1rem;
  width: 100%;
  position: fixed;
  bottom: 0;
}
</style>


