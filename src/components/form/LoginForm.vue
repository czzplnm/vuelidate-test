<template>
  <div id="login-form">
    <input-template
        name="username"
        :model-value="this.username"
        :rules="this.rules"
        label="Username"
    >
    </input-template>

    <input-template
        name="password"
        :model-value="this.password"
        :rules="this.rules"
        label="Password"
    >
    </input-template>

    <button type="submit" @click="login()">Login</button>
  </div>
</template>

<script lang="ts">
  import InputTemplate from "@/components/templates/InputTemplate.vue";
  import {useVuelidate} from "@vuelidate/core";
  import {ref} from 'vue'
  import {required, maxLength} from "@vuelidate/validators";

  export default {
    name: 'LoginForm',
    components: {InputTemplate},

    setup() {
      const password = ref(undefined)
      const username = ref(undefined)

      const rules = {
        username: {
          required,
        },
        password: {
          required,
          maxLength: maxLength(49)
        }
      }

      const v = useVuelidate()

      return {username, password, rules, v}
    },

    methods: {
      login() {
        console.log('Logging in');


        this.v.$dirty = true
        this.v.$touch();
        if (this.v.$invalid) {
          console.log('Invalid form');
        } else {
          console.log('Valid form');
        }
      }
    }
  }
</script>

<style scoped>
  #login-form {
    margin: 20px;
    text-align: center;
  }

  button {
    width: 50%;
    margin: 10px;
    padding: 10px;
  }
</style>