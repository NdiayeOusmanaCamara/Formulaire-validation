<template>
    <div class="body">
      <form @submit.prevent="handleSubmit">
        <h1>Formulaire de saisir</h1>
        <div>
          <label for="name">Nom :</label>
          <input
            type="text"
            id="name"
            v-model="form.name"
            :class="{ 'is-invalid': errors.name }"
          />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>
        <div>
          <label for="email">Email :</label>
          <input
            type="email"
            id="email"
            v-model="form.email"
            :class="{ 'is-invalid': errors.email }"
          />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>
        <div>
          <label for="phone">Numéro de téléphone :</label>
          <input
            type="text"
            id="phone"
            v-model="form.phone"
            :class="{ 'is-invalid': errors.phone }"
          />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>
        <button type="submit">Soumettre</button>
      </form>
      <div v-if="successMessage" class="success">
        {{ successMessage }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        form: {
          name: '',
          email: '',
          phone: '',
        },
        errors: {},
        successMessage: '',
      };
    },
    methods: {
      validateForm() {
        this.errors = {};
        if (!this.form.name) this.errors.name = 'Le nom est requis.';
        if (!this.form.email) {
          this.errors.email = 'L\'email est requis.';
        } else if (!/\S+@\S+\.\S+/.test(this.form.email)) {
          this.errors.email = 'L\'email doit être valide.';
        }
        if (!this.form.phone) {
          this.errors.phone = 'Le numéro de téléphone est requis.';
        } else if (!/^\d{8}$/.test(this.form.phone)) {
          this.errors.phone = 'Le numéro de téléphone doit contenir 8 chiffres.';
        }
        return Object.keys(this.errors).length === 0;
      },
      handleSubmit() {
        if (this.validateForm()) {
          this.successMessage = 'Formulaire soumis avec succès!';
          this.form.name = '';
          this.form.email = '';
          this.form.phone = '';
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .body {
    background-color: #8c2377;
    height: 90vh;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0;
  }

  form {
    max-width: 500px;
    padding: 2em;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
    font-family: 'Arial', sans-serif;
  }

  h1 {
    text-align: center;
    color: #651956;
    margin-bottom: 1.5em;
    font-size: 1.5em;
    font-weight: bold;
  }

  label {
    display: block;
    margin-bottom: 0.5em;
    font-weight: bold;
    color: #333;
  }

  input {
    width: 100%;
    padding: 0.75em;
    margin-bottom: 1.5em;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-sizing: border-box;
    transition: border-color 0.3s, box-shadow 0.3s;
    outline: none;
  }

  input:focus {
    border-color: #5bc0de;
    outline: none;
  }

  .error {
    color: #d9534f;
    font-size: 0.875em;
    margin-top: -1em;
    margin-bottom: 1em;
  }

  .is-invalid {
    border-color: #d9534f;
  }

  button {
    display: inline-block;
    width: 100%;
    padding: 0.75em;
    font-size: 1em;
    color: #fff;
    background-color: #651956;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
  }

  button:hover {
    background-color: #31d586;
    transform: scale(1.05);
  }

  .success {
    padding: 1em;
    color: #fff;
    background-color: #31d586;
    border-radius: 5px;
    text-align: center;
    margin-top: 1.5em;
    font-size: 1.2em;
    margin-left: 40px;
  }
</style>
