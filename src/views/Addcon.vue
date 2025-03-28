<script setup lang="ts">
import ContactForm from "@/components/ContactForm.vue";
import { useRouter } from "vue-router";

interface Contact {
  id: number;
  firstName: string;
  lastName: string;
  email: string;
  phone: string;
  address: string;
}

const router = useRouter();

const addNewContact = (contact: Contact) => {
  const contactList: Contact[] = JSON.parse(localStorage.getItem("contacts") || "[]");
  contactList.push(contact);
  localStorage.setItem("contacts", JSON.stringify(contactList));
  router.push("/");
};
</script>

<template>
  <div class="contact-container">
    <h2>Add New Contact</h2>
    <ContactForm @submit="addNewContact" />
  </div>
</template>

<style scoped>
/* Container */
.contact-container {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  background: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  text-align: center;
}

/* Header */
h2 {
  font-size: 26px;
  color: #333;
  margin-bottom: 15px;
  border-bottom: 3px solid #4c62f3;
  padding-bottom: 10px;
  display: inline-block;
  font-weight: 600;
}
</style>
