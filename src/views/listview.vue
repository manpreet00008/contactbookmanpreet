<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";
import ContactList from "@/components/ContactList.vue";

const router = useRouter();
const searchTerm = ref("");

const navigateToAddContact = () => {
  router.push("/add");
};
</script>

<template>
  <div class="container">
    <header class="header">
      <h1>Contact Book</h1>
    </header>

    <div class="search-container">
      <input v-model="searchTerm" placeholder="Search contacts..." class="search-input" />
      <button @click="navigateToAddContact" class="add-btn">+ Add Contact</button>
    </div>

    <ContactList :search-query="searchTerm" />
  </div>
</template>

<style scoped>
/* Reset Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Page Container */
.container {
  max-width: 800px;
  margin: 40px auto;
  padding: 20px;
  background: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

/* Header */
.header {
  text-align: center;
  background: #4c62f3;
  color: white;
  padding: 15px;
  border-radius: 10px 10px 0 0;
}

.header h1 {
  font-size: 30px;
}

/* Search & Add Section */
.search-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #e0e0e0;
  padding: 12px;
  border-radius: 0 0 10px 10px;
  margin-bottom: 20px;
}

.search-input {
  flex-grow: 1;
  font-size: 18px;
  padding: 8px;
  border: none;
  border-radius: 5px;
}

.add-btn {
  padding: 10px 15px;
  margin-left: 10px;
  background: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background 0.3s ease;
}

.add-btn:hover {
  background: #218838;
}
</style>
