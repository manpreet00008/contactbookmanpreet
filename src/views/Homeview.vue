<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";
import ContactList from "@/components/ContactList.vue";

const router = useRouter();
const searchTerm = ref("");

const navigateToAdd = () => {
  router.push("/add");
};
</script>

<template>
  <div class="container">
    <header>
      <h1>Contact Manager</h1>
    </header>

    <nav>
      <a href="#" @click.prevent="navigateToAdd">➕ Add Contact</a>
    </nav>

    <div class="search-container">
      <input v-model="searchTerm" placeholder="🔍 Search contacts..." />
    </div>

    <ContactList :search-query="searchTerm" />
  </div>
</template>

<style scoped>
/* Reset default styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Arial", sans-serif;
}

/* Layout container */
.container {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Header */
header h1 {
  font-size: 32px;
  color: #333;
  padding: 10px 0;
  border-bottom: 3px solid #4c62f3;
}

/* Navigation */
nav {
  display: flex;
  justify-content: center;
  background: #4c62f3;
  padding: 15px;
  border-radius: 8px;
  margin-top: 20px;
}

nav a {
  color: white;
  font-size: 18px;
  text-decoration: none;
  transition: 0.3s;
}

nav a:hover {
  color: yellow;
}

/* Search Box */
.search-container {
  width: 100%;
  margin: 20px auto;
  display: flex;
  justify-content: center;
}

.search-container input {
  width: 80%;
  padding: 10px;
  font-size: 18px;
  border: 2px solid #ccc;
  border-radius: 25px;
  outline: none;
  text-align: center;
}

.search-container input:focus {
  border-color: #4c62f3;
}
</style>
