<script setup lang="ts">
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";

interface ContactInfo {
  id: number;
  firstName: string;
  lastName: string;
  email: string;
  phone: string;
  address: string;
}

const route = useRoute();
const router = useRouter();
const selectedContact = ref<ContactInfo | null>(null);

onMounted(() => {
  const storedContacts = JSON.parse(localStorage.getItem("contacts") || "[]");
  selectedContact.value = storedContacts.find(
    (contact: ContactInfo) => contact.id === Number(route.params.id)
  );
});

const handleDelete = () => {
  const updatedContacts = JSON.parse(localStorage.getItem("contacts") || "[]").filter(
    (contact: ContactInfo) => contact.id !== Number(route.params.id)
  );
  localStorage.setItem("contacts", JSON.stringify(updatedContacts));
  router.push("/");
};
</script>

<template>
  <div v-if="selectedContact" class="contact-profile">
    <div class="contact-header">
      <img src="https://via.placeholder.com/100" alt="Profile" class="profile-image" />
      <h2>{{ selectedContact.firstName }} {{ selectedContact.lastName }}</h2>
    </div>

    <div class="contact-details">
      <p><strong>Email:</strong> {{ selectedContact.email }}</p>
      <p><strong>Phone:</strong> {{ selectedContact.phone }}</p>
      <p><strong>Address:</strong> {{ selectedContact.address }}</p>
    </div>

    <div class="action-buttons">
      <button class="btn edit-btn" @click="$router.push(`/edit/${selectedContact.id}`)">Edit</button>
      <button class="btn delete-btn" @click="handleDelete">Delete</button>
    </div>
  </div>
</template>

<style scoped>
/* Profile Card */
.contact-profile {
  max-width: 450px;
  margin: 50px auto;
  padding: 25px;
  background: #ffffff;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Header Section */
.contact-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.profile-image {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 4px solid #007bff;
}

/* Contact Details */
.contact-details {
  margin-top: 20px;
  text-align: left;
  font-size: 16px;
  line-height: 1.6;
}

.contact-details p {
  background: #f8f9fa;
  padding: 10px;
  border-radius: 6px;
  margin: 8px 0;
}

/* Action Buttons */
.action-buttons {
  margin-top: 25px;
  display: flex;
  justify-content: center;
  gap: 15px;
}

.btn {
  padding: 12px 18px;
  border: none;
  cursor: pointer;
  border-radius: 6px;
  font-size: 15px;
  font-weight: bold;
  transition: all 0.3s ease-in-out;
}

.edit-btn {
  background: #007bff;
  color: white;
}

.edit-btn:hover {
  background: #0056b3;
}

.delete-btn {
  background: #dc3545;
  color: white;
}

.delete-btn:hover {
  background: #a71d2a;
}
</style>
