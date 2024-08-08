<template>
    <h1>Formulaire de saisir</h1>
    <div>
      <form @submit.prevent="handleSubmit">
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
          // Vous pouvez également ajouter du code pour envoyer les données à un serveur ici
          // reset the form
          this.form.name = '';
          this.form.email = '';
          this.form.phone = '';
        }
      },
    },
  };
  </script>
  
  <style scoped>
  form {
    max-width: 600px;
    margin: 0 auto;
    padding: 1.5em;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  h1{
    text-align: center;
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
    margin-bottom: 1em;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    transition: border-color 0.3s;
  }
  
  
  .error {
    color: #d9534f;
    font-size: 0.875em;
    margin-top: 0.25em;
  }
  
  
  .is-invalid {
    border-color: #d9534f;
  }
  
  
  button {
    display: inline-block;
    padding: 0.75em 1.5em;
    font-size: 1em;
    color: #fff;
    background-color: #5bc0de;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  button:hover {
    background-color: #31b0d5;
  }
  
  
  .success {
    margin-bottom: 400px;
    padding: 0.75em;
    color: #fff;
    background-color: #5bc0de;
    border-radius: 4px;
    text-align: center;
    width: 50%;
    margin: 40px auto;
    
  }
  </style>
  