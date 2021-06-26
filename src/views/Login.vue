<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-container>
      <v-card class="mx-auto my-12">
        <v-card-text>
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>

          <v-text-field
            v-model="password"
            :rules="passwordRules"
            type="password"
            label="password"
            required
          ></v-text-field>
          
        </v-card-text>

        <v-card-actions>
          <v-btn color="blue" @click="handleLogin"> Validate </v-btn>
        </v-card-actions>
      
      </v-card>
      <p v-text="errors.email"></p>
      <p v-text="errors.password"></p>
    </v-container>
  </v-form>
</template>
<script>
import axios from "axios";
axios.defaults.withCredentials = true;
axios.defaults.baseURL = "http://api.larawithsanctum.test/";

export default {
  name: "Login",
  data: () => ({
    valid: false,

    email: "",
    password: "",
    errors: {},
    passwordRules: [
      (v) => !!v || "Password is required",
      (v) => v.length >= 1 || "Password is invalid",
    ],
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+/.test(v) || "E-mail must be valid",
    ],
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
    },
    handleLogin() {
      alert(this.email);
      alert(this.password);
      axios.get('/sanctum/csrf-cookie').then((res) => {
        axios
          .post('/api/authenticate', {
            email: this.email,
            password: this.password,
            device_name: 'browser',
          })
          .then((response) => {
            console.log(response)
            localStorage.setItem('token',response.data)
            this.$router.push('/')
            console.log(res);
          })
          .catch((errors) => {
            this.errors = errors.response.data.errors;
          });
      });
    },
  },
};
</script>

