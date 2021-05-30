<template>
<v-form
    ref="form"
    v-model="valid"
    lazy-validation
 >
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
            <v-btn
              color="blue"
              @click="handleLogin"
              type="submit"
              >
                Validate
            </v-btn>
          </v-card-actions>
        </v-card>
    </v-container>
    </v-form>
</template>
<script>

import axios from 'axios';
axios.defaults.withCredentials= true;
axios.defaults.baseURL = "http://127.0.0.1:8000/";
export default {
    name:'Login',
    data: () => ({
      valid: false,
      password: '',
      passwordRules: [
        v => !!v || 'Password is required',
        v => v.length >= 5 || 'Password is invalid',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }),
     methods: {
      validate () {
        this.$refs.form.validate()
        
      },
      handleLogin() {
        alert(this.email);
        alert(this.password);
        axios.get('/sanctum/csrf-cookie').then(response => {
          axios.post('/api/authenticate', {email: this.email, password: this.password})
            .then( (res) => {
                console.log(res);
              })
              .catch( (err) => {
                console.log(err);
              })
        });
      },
     }   
}
</script>