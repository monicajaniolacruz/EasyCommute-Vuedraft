<script setup>
import { ref } from 'vue'
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
const drawer = ref(false)
const zoomedImage = ref(null)
const showModal = ref(false)

const openModal = (image) => {
  zoomedImage.value = image
  showModal.value = true
}

const closeModal = () => {
  zoomedImage.value = null // Reset image when closing
  showModal.value = false
}
</script>

<template>
  <v-app>
    <!-- Background Video -->
    <div class="video-container">
      <video autoplay muted loop class="background-video">
        <source src="/images/background.mp4" type="video/mp4" />
      </video>
    </div>

    <!-- Header Section -->
    <v-app-bar app flat class="transparent-navbar">
      <v-container class="d-flex align-center">
        <!-- Logo -->
        <v-app-bar-title class="text-h5 font-weight-bold white-text-custom">
          Easy Commute
        </v-app-bar-title>

        <!-- Navigation -->
        <v-spacer></v-spacer>
        <nav v-if="!mobile">
          <router-link to="/home" class="nav-link">Home</router-link>
          <router-link to="/routes" class="nav-link">Ride</router-link>
          <router-link to="#" class="nav-link">Fare</router-link>
          <router-link to="/contact" class="nav-link">Contact Us</router-link>
          <router-link to="/profile" class="nav-link">Profile</router-link>
        </nav>
        <v-btn icon v-if="mobile" @click="drawer = !drawer">
          <v-icon color="white">mdi-menu</v-icon>
        </v-btn>
      </v-container>
    </v-app-bar>

    <!-- Drawer for Mobile Navigation -->
    <v-navigation-drawer v-model="drawer" temporary class="mobile-drawer">
      <v-list>
        <v-list-item>
          <router-link to="#" class="nav-link">Home</router-link>
        </v-list-item>
        <v-list-item>
          <router-link to="/routes" class="nav-link">Ride</router-link>
        </v-list-item>
        <v-list-item>
          <router-link to="#" class="nav-link">Fare</router-link>
        </v-list-item>
        <v-list-item>
          <router-link to="/contact" class="nav-link">Contact Us</router-link>
        </v-list-item>
        <v-list-item>
          <router-link to="/profile" class="nav-link">Profile</router-link>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- Images Overlay -->
    <div class="image-container">
      <img
        src="/images/tricyclefare.png"
        alt="Tricycle Fare"
        class="overlay-image"
        @click="openModal('/images/tricyclefare.png')"
      />
      <img
        src="/images/multicabfare.jpg"
        alt="Multicab Fare"
        class="overlay-image"
        @click="openModal('/images/multicabfare.jpg')"
      />
    </div>

    <!-- Fullscreen Zoomed Image -->
    <v-dialog
      v-model="showModal"
      fullscreen
      overlay-color="black"
      transition="fade-transition"
      persistent
    >
      <v-img :src="zoomedImage" class="zoomed-image" @click="closeModal"></v-img>
    </v-dialog>

    <RouterView />
  </v-app>
</template>

<style scoped>
/* Background Video */
.background-video {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  z-index: -1;
}

/* Video Container */
.video-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

/* Navbar Styles */
.transparent-navbar {
  background-color: transparent;
}

.nav-link {
  color: white;
  text-decoration: none;
  margin-right: 50px;
  font-weight: 500;
  transition: opacity 0.3s ease;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva,
    Verdana, sans-serif;
}

.nav-link:hover {
  opacity: 0.8;
}

.white-text-custom {
  color: white !important;
}

/* Image Container and Overlay Images */
.image-container {
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  z-index: 1;
}

.overlay-image {
  width: 80%;
  max-width: 600px;
  border-radius: 10px;
  cursor: pointer;
}

/* Zoomed Image */
.zoomed-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  background-color: black;
  cursor: zoom-out;
}

/* Mobile Responsiveness */
@media (max-width: 600px) {
  .overlay-image {
    width: 90%;
  }
}
</style>
