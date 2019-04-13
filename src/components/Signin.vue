<script>
import axios from "axios";

export default {
  name: "Signin",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    onSubmit() {
      const credentials = { email: this.email, password: this.password };
      axios
        .post("http://localhost:5000/api/auth/signin", credentials)
        .then(res => this.$emit("on-auth", res.data))
        .catch(err => console.log(err));
    }
  }
};
</script>


<template>
  <div class="signin-form">
    <div class="form-group space">
      <label for="exampleInputEmail1">Email address</label>
      <input
        v-model="email"
        type="email"
        class="form-control"
        id="exampleInputEmail1"
        aria-describedby="emailHelp"
        placeholder="Enter email"
      >
    </div>
    <div class="form-group space">
      <label for="exampleInputPassword1">Password</label>
      <input
        v-model="password"
        type="password"
        class="form-control"
        id="exampleInputPassword1"
        placeholder="Password"
      >
    </div>

    <button type="submit" v-on:click="onSubmit" class="btn btn-primary space">Submit</button>
  </div>
</template>

<style>
.signin-form {
  margin: 100px auto;
  width: 500px;
}

.space {
  margin: 0 0 30px 0;
}
</style>
