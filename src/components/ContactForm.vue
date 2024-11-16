<template>
  <form @submit.prevent="handleSubmit">
    <div>
      <label for="firstName">First Name:</label>
      <input
        id="firstName"
        v-model="contact.firstName"
        type="text"
        placeholder="Enter first name"
        required
      />
    </div>

    <div>
      <label for="lastName">Last Name:</label>
      <input
        id="lastName"
        v-model="contact.lastName"
        type="text"
        placeholder="Enter last name"
        required
      />
    </div>

    <div>
      <label for="email">Email:</label>
      <input
        id="email"
        v-model="contact.email"
        type="email"
        placeholder="Enter email"
        required
      />
    </div>

    <div>
      <label for="phone">Phone Number:</label>
      <input
        id="phone"
        v-model="contact.phone"
        type="tel"
        placeholder="Enter phone number"
      />
    </div>

    <div>
      <label for="address">Address:</label>
      <textarea
        id="address"
        v-model="contact.address"
        placeholder="Enter address"
      ></textarea>
    </div>

    <button type="submit">{{ isEditing ? "Update Contact" : "Add Contact" }}</button>
    <button type="button" @click="cancel">Cancel</button>
  </form>
</template>

<script>
export default {
  props: {
    existingContact: {
      type: Object,
      default: () => ({
        firstName: "",
        lastName: "",
        email: "",
        phone: "",
        address: "",
      }),
    },
    isEditing: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      contact: { ...this.existingContact },
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("submit", { ...this.contact });
    },
    cancel() {
      this.$emit("cancel");
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

label {
  font-weight: bold;
}

input,
textarea {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button[type="submit"] {
  background-color: #007bff;
  color: white;
}

button[type="button"] {
  background-color: #ccc;
}
</style>
