<template>
  <div class="landing">
    <button @click="logout">logout</button>
    <h1>Hello{{ name }}</h1>
    <h2>email {{ email }}</h2>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "landing",
  data() {
    return {
      name: "",
      email: "",
    };
  },
  created() {
    if (localStorage.getItem("token") === null) {
      this.$router.push("/login");
    }
  },
  mounted() {
    axios
      .get("http://localhost:5000/user", {
        headers: { token: localStorage.getItem("token") },
      })
      .then((res) => {
        console.log(res);
        this.name = res.data.user.name;
        this.email = res.data.user.email;
      });
  },
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push("/login");
    },
  },
};
</script>

<style scoped></style>
