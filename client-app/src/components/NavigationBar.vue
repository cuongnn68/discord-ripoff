<template>
  <div class="nav">
    <router-link to="/" class="logo">LOGO</router-link>
    <router-link class="link" to="/">Home</router-link>
    <router-link class="link" to="/about">About</router-link>
    <router-link class="link" to="/chat">Chat</router-link>
    <router-link class="link" to="/search">Search</router-link>
    <router-link class="link" to="/test">Test</router-link>
    <!-- <router-link class="link" to="/add-room">Add Room</router-link>
    <router-link class="link" to="/add-friend">Add Friend</router-link> -->
    <div class="empty"></div>
    <router-link v-if="!login" class="link" to="/login">Login</router-link>
    <router-link v-if="!login" class="link" to="/register">Register</router-link>
    <router-link v-if="login" class="link" v-bind:to="'/user/'+userIdMethod()">Info</router-link>
    <div v-if="login" v-on:click="logout" class="link">Logout</div>
  </div>
</template>

<script>
import {logout} from "../api/userAPI.js";
import * as storage from "../utils/storage.js";
export default {
  name: "NavBar",
  props: [
    "login"
  ],
  data: function() {
    return {
      // userId: 0,
      // login: true,
    }
  },
  computed: {
    userId() {
      return storage.getUser().id; // FIXME: not update, had to use method instead of this
    }
    // loginActive: function() {
    //   return this.login;
    // }
  },
  methods: {
    logout() {
      logout();
      localStorage.removeItem("userInfo");
      this.$emit('logout');
      this.$router.push("/login");
      this.$emit("newNoti", {content: "Loged out", type: "green"});
    },
    userIdMethod() {
      return storage.getUser().id;
    }
  }
}
</script>

<style>
  .nav {
    background-color: white;
    height: 60px;
    box-shadow: 0px 5px 8px lightgray;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
  }
  .logo {
    text-decoration-line: none;
    padding: 0rem 2rem 0rem 2rem;
    line-height: 60px; 
    color:#b15ebb;
    font-size: 40px;
    font-weight: 900;
  }
  .link {
    text-decoration-line: none;
    padding: 0rem 0.6rem 0rem 0.6rem;
    line-height: 60px;
    color: #5f566d;
    font-size: 20px;
    /* transition-duration: 0.35s; */
    cursor: pointer;
  }
  .link:hover {
    background-color:#b15ebb;
    color: white;
  }
  .empty {
    flex: 1 1;
  }
  

  .go-to-outside-test {
    background-color: red;
  }
</style>