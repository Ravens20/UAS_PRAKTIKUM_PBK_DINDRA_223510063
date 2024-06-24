<template>
  <div :class="['sidebar', { 'sidebar-hidden': isHidden }]">
    <div class="sidebar-header">
      <i class="fas fa-book logo"></i>
      <h1 class="app-name">Project/Tugas</h1>
    </div>
    <div class="sidebar-profile">
      <img src="../assets/images/profile.jpg" alt="Profile Picture" class="profile-pic">
      <h2 class="profile-name">Dindra Desvantio</h2>
    </div>
    <hr class="divider">
    <div class="sidebar-content">
      <ul>
        <li class="task-item"><a href="https://223510063-dindra-tugas1.netlify.app" target="_blank"><i class="fas fa-book"></i> Tugas 1</a></li>
        <li class="task-item"><a href="https://223510063-dindra-tugas2.netlify.app" target="_blank"><i class="fas fa-book"></i> Tugas 2</a></li>
        <li class="task-item"><a href="https://223510063-dindra-tugas3.netlify.app" target="_blank"><i class="fas fa-book"></i> Tugas 3</a></li>
        <li class="task-item"><a href="https://223510063-dindra-tugas4.netlify.app" target="_blank"><i class="fas fa-book"></i> Tugas 4</a></li>
        <li class="task-item"><a href="https://223510063-dindra-tugas5.netlify.app" target="_blank"><i class="fas fa-book"></i> Tugas 5</a></li>
        <li class="task-item"><a href="https://223510063-dindraa.netlify.app" target="_blank"><i class="fas fa-book"></i> Tugas 6</a></li>
      </ul>
      <hr class="divider">
      <div class="sidebar-social">
        <a href="#"><i class="fab fa-facebook-f"></i></a>
        <a href="#"><i class="fab fa-twitter"></i></a>
        <a href="#"><i class="fab fa-linkedin-in"></i></a>
        <a href="#"><i class="fab fa-instagram"></i></a>
      </div>
    </div>
    <div class="sidebar-footer">
      <p>Contact us: info@example.com</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
  props: {
    isHidden: {
      type: Boolean,
      default: true
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css');

.sidebar {
  width: 250px;
  background: linear-gradient(to bottom, #3a6186, #89253e);
  padding: 1rem 0.5rem;
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease, width 0.3s ease;
  z-index: 1000;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 20px;
  font-family: 'Roboto', sans-serif;
  display: flex;
  flex-direction: column;
}

.sidebar.sidebar-hidden {
  transform: translateX(-110%);
}

.sidebar-header {
  display: flex;
  align-items: center;
  padding: 1rem;
  text-align: center;
  margin-bottom: 1rem;
}

.logo {
  font-size: 2rem;
  color: #fff;
  margin-right: 0.5rem;
}

.app-name {
  font-size: 1.5rem;
  color: #fff;
}

.sidebar-profile {
  text-align: center;
  margin-bottom: 1rem;
}

.profile-pic {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-bottom: 0.5rem;
}

.profile-name {
  font-size: 1.2rem;
  color: #fff;
}

.divider {
  border: none;
  border-top: 1px solid rgba(255, 255, 255, 0.3);
  margin: 1rem 0;
}

.sidebar-content {
  flex: 1;
  overflow-y: auto;
}

.sidebar ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.sidebar ul li {
  margin: 0.5rem 0;
}

.sidebar ul li a {
  color: #fff;
  text-decoration: none;
  font-size: 1.1rem;
  display: flex;
  align-items: center;
  padding: 0.5rem 1rem;
  transition: background-color 0.3s ease, color 0.3s ease;
  border-radius: 10px;
}

.sidebar ul li a i {
  margin-right: 0.5rem;
}

.sidebar ul li a:hover {
  background-color: rgba(255, 255, 255, 0.3);
  color: #fff;
}

.task-item a {
  background-color: #2980b9;
}

.task-item a:hover {
  opacity: 0.8;
}

.sidebar-social {
  text-align: center;
  margin-bottom: 1rem;
}

.sidebar-social a {
  color: #fff;
  font-size: 1.2rem;
  margin: 0 0.5rem;
  transition: color 0.3s ease;
}

.sidebar-social a:hover {
  color: #ddd;
}

.sidebar-footer {
  text-align: center;
  color: #fff;
  font-size: 0.9rem;
  padding: 0 0.5rem;
}
</style>
