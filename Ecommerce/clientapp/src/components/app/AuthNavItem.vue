<template>
  <b-nav-item-dropdown v-if="isAuthenticated" right>
    <template slot="button-content">
      <!-- <i class="fas fa-user"></i> -->
      <font-awesome-icon icon="user" />
      {{ fullName }}
    </template>
    <b-dropdown-item item v-if="isCustomer" to="/account">
      <!-- <i class="fas fa-user"></i> -->
      <font-awesome-icon icon="user" />
      My Account
    </b-dropdown-item>
    <b-dropdown-item @click="logout">
      <!-- <i class="fas fa-sign-out-alt"></i> -->
      <font-awesome-icon icon="sign-out-alt" />
      Logout
    </b-dropdown-item>
  </b-nav-item-dropdown>
  <b-nav-item v-else @click="login">
    <!-- <i class="fas fa-user"></i> -->
    <font-awesome-icon icon="user" />
    Login / register
  </b-nav-item>
</template>

<script>
export default {
  name: "auth-nav-item",
  computed: {
    isAuthenticated() {
      return this.$store.getters.isAuthenticated;
    },
    isCustomer() {
      return this.$store.getters.isInRole("Customer");
    },
    fullName() {
      return `${this.$store.state.auth.firstName} ${this.$store.state.auth.lastName}`;
    },
  },
  methods: {
    login() {
      this.$store.commit("showAuthModal");
    },
    logout() {
      this.$store.dispatch("logout").then(() => {
        if (this.$route.matched.some((route) => route.meta.requiresAuth)) {
          this.$router.push("/");
        }
      });
    },
  },
};
</script>
