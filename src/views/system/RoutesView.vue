<script setup>
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
</script>
<template>
  <v-app>
    <!-- Background Video -->
    <div class="video-container">
      <video autoplay muted loop class="background-video">
        <source src="/public/images/home.mp4" type="video/mp4" />
      </video>
    </div>
    <v-app-bar app flat class="transparent-navbar">
      <v-container class="d-flex align-center">
        <!-- Logo -->
        <v-app-bar-title class="text-h5 font-weight-bold white-text-custom">
          Easy Commute
        </v-app-bar-title>

        <!-- Spacer -->
        <v-spacer></v-spacer>

        <!-- Desktop Navigation -->
        <nav v-if="!mobile" class="desktop-nav">
          <router-link to="/home" class="nav-link">Home</router-link>
          <router-link to="#" class="nav-link">Ride</router-link>
          <router-link to="/fare" class="nav-link">Fare</router-link>
          <router-link to="/contact" class="nav-link">Contact Us</router-link>
          <router-link to="/profile" class="nav-link">Profile</router-link>
        </nav>

        <!-- Mobile Menu Icon -->
        <v-btn icon v-else @click="drawer = !drawer">
          <v-icon color="white">mdi-menu</v-icon>
        </v-btn>
      </v-container>
    </v-app-bar>

    <!-- Mobile Drawer -->
    <v-navigation-drawer v-model="drawer" temporary>
      <v-list>
        <v-list-item>
          <router-link to="#" class="nav-link">Home</router-link>
        </v-list-item>
        <v-list-item>
          <router-link to="/complain" class="nav-link">Complain</router-link>
        </v-list-item>
        <v-list-item>
          <router-link to="/contact" class="nav-link">Contact Us</router-link>
        </v-list-item>
        <v-list-item>
          <router-link to="#" class="nav-link">Profile</router-link>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <!-- First Row -->
    <v-container class="text-center custom-container">
      <v-row justify="center" align="center" class="button-row first-row">
        <v-col cols="12" md="4" sm="6">
          <RouterLink to="/multicab" style="text-decoration: none">
            <v-btn class="custom-btn" rounded="xl" size="x-large" block> Multicab </v-btn>
          </RouterLink>
        </v-col>
      </v-row>

      <!-- Second Row -->
      <v-row justify="center" align="center" class="button-row second-row">
        <v-col cols="12" md="4" sm="6">
          <RouterLink to="/tricycle" style="text-decoration: none">
            <v-btn class="custom-btn" rounded="xl" size="x-large" block> Tricycle </v-btn>
          </RouterLink>
        </v-col>
      </v-row>
    </v-container>

    <RouterView />
  </v-app>
</template>
<style scoped>
.background-video {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  z-index: -1;
}
.video-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.logo {
  font-size: 2em;
  color: white;
  user-select: none;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva,
    Verdana, sans-serif;
}

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

.white-text-custom {
  color: white !important;
}

.custom-btn {
  font-weight: bold; /* Adjust font weight for a bolder appearance */
  padding: 16px 24px; /* Increase padding for a 'heavier' feel */
  border: 3px solid #ffffff; /* Add a thicker border */
  background-color: #ffffff; /* Button background color */
  color: #000000; /* Text color */
  text-transform: uppercase; /* Optional: Make text uppercase */
  transition: all 0.3s ease; /* Smooth transitions for hover effects */
}

.custom-btn:hover {
  background-color: #000000; /* Change background on hover */
  color: #ffffff; /* Change text color on hover */
  border-color: #000000; /* Change border color on hover */
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.2); /* Add shadow for hover effect */
}

.button-row {
  margin-top: 20px; /* Add some spacing between rows */
}

.first-row {
  transform: translate(32%, 150%);
  width: 60%;
}

.second-row {
  transform: translate(32%, 300%);
  width: 60%;
}

</style>
