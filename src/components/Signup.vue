<template>
  <div class="signup">
    Name: <input v-model="name" type="text" /><br />
    email: <input v-model="email" type="text" /><br />
    password: <input v-model="password" type="text" /><br />
    <button @click="signup">signup</button>
    {{ error }}
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "signup",
  data() {
    return {
      name: "",
      email: "",
      password: "",
      error: "",
    };
  },
  methods: {
    signup() {
      let newUser = {
        name: this.name,
        email: this.email,
        password: this.password,
      };
      axios.post("http://localhost:5000/signup", newUser).then(
        (res) => {
          console.log(res);
          this.error = "";
          this.$router.push("/login");
        },
        (err) => {
          console.log(err.response);
          this.error = err.response.data.error;
        }
      );
    },
  },
};
</script>

<style scoped></style>
