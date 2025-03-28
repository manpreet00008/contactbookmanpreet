<script setup lang="ts">
import ContactForm from "@/components/ContactForm.vue";
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";

interface Contact {
  id: number;
  firstName: string;
  lastName: string;
  email: string;
  phone: string;
  address: string;
}

const route = useRoute();
const router = useRouter();
const selectedContact = ref<Contact | null>(null);

onMounted(() => {
  const contactList: Contact[] = JSON.parse(localStorage.getItem("contacts") || "[]");
  selectedContact.value = contactList.find((c) => c.id === Number(route.params.id)) || null;
});

const saveUpdatedContact = (updatedContact: Contact) => {
  let contactList: Contact[] = JSON.parse(localStorage.getItem("contacts") || "[]");
  contactList = contactList.map((c) => (c.id === updatedContact.id ? updatedContact : c));
  localStorage.setItem("contacts", JSON.stringify(contactList));
  router.push("/");
};
</script>

<template>
  <div class="edit-contact-container" v-if="selectedContact">
    <h2>Edit Contact</h2>
    <ContactForm :contact="selectedContact" @submit="saveUpdatedContact" />
  </div>
</template>

<style scoped>
/* Main Container */
.edit-contact-container {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Title */
h2 {
  color: #333;
  font-size: 24px;
  margin-bottom: 20px;
}
</style>
