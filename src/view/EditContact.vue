<template>
  <div>
    <h2>Edit Contact</h2>
    <form @submit.prevent="updateContact">
      <input v-model="firstName" placeholder="First Name" required />
      <input v-model="lastName" placeholder="Last Name" required />
      <input v-model="email" placeholder="Email" type="email" required />
      <input v-model="phone" placeholder="Phone" />
      <button type="submit">Update Contact</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    const id = this.$route.params.id;
    const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
    const contact = contacts.find(c => c.id === id);
    return { ...contact };
  },
  methods: {
    updateContact() {
      const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      const index = contacts.findIndex(c => c.id === this.$route.params.id);
      if (index !== -1) {
        contacts[index] = { ...contacts[index], firstName: this.firstName, lastName: this.lastName, email: this.email, phone: this.phone };
        localStorage.setItem('contacts', JSON.stringify(contacts));
        this.$router.push(`/contact/${this.$route.params.id}`);
      }
    }
  }
};
</script>
