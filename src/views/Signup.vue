<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newUser.name" />
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="newUser.email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="newUser.password" />
      </div>
      <div>
        <label>Password Confirmation:</label>
        <input type="password" v-model="newUser.password_confirmation" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data: function () {
      return {
        newUser: {},
        errors: []
      };
    },
    methods: {
      submit: function () {
        axios
          .post("/users", this.newUser)
          .then((response) => {
            console.log(response.data);
            this.$router.push("/login");
          })
          .catch((error) => {
            this.errors = error.response.data.errors;
          });
      }
    }
  };
</script>

        

