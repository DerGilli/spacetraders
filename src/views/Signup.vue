<template>
  <div class="container">
    <div class="form-wrapper">
      <label for="username">username:</label>
      <input type="text" name="username" id="username" v-model="username" />
      <button @click="handleSignup">Sign Up</button>
      <span
        >Already have an Account?
        <router-link to="/Login">Log in</router-link>
      </span>
    </div>
  </div>
</template>

<script lang="ts">
import router from "@/router";
import { defineComponent, ref } from "vue";
import { createNewUser } from "../api";
import useUser from "../Auth";

export default defineComponent({
  setup() {
    const { login } = useUser();
    const username = ref("");

    const handleSignup = async () => {
      try {
        const token = await createNewUser(username.value);
        login(username.value, token);
        router.push("/");
      } catch (error) {
        console.log(error.message);
      }
    };

    return { username, handleSignup };
  }
});
</script>

<style scoped>
.form-wrapper {
  display: flex;
  background: #969696;
  flex-direction: column;
  padding: 15px 30px;
}
input {
  margin-bottom: 10px;
  color: black;
}
span {
  margin-top: 20px;
  font-size: 10px;
  text-align: center;
}
</style>
