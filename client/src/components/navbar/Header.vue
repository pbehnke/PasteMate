<template>
  <b-navbar type="inverse" class="navbar-expand-lg navbar-absolute">
    <b-container fluid>
      <div class="navbar-wrapper">
        <div v-bind:class="{toggled : sideOpen}" class="navbar-toggle d-inline">
          <button v-on:click="openSideBar()" type="button" class="navbar-toggler">
            <span class="navbar-toggler-bar bar1"></span>
            <span class="navbar-toggler-bar bar2"></span>
            <span class="navbar-toggler-bar bar3"></span>
          </button>
        </div>
        <b-link to="/" class="navbar-brand">PasteMate</b-link>
      </div>
      <b-navbar-nav class="ml-auto">
        <b-nav-item-dropdown right id="dropdown-menu">
          <template v-if="user">
            <template slot="button-content">
              <strong>{{ user.username }}</strong>
            </template>
            <b-link to="/account/manage" class="dropdown-item">Manage Account</b-link>
            <b-link to="/account/signout" class="dropdown-item">Sign Out</b-link>
          </template>
          <template v-else>
            <template slot="button-content">
              <strong>Account</strong>
            </template>
            <b-link to="/account/signin" class="dropdown-item">Sign In</b-link>
            <b-link to="/account/signup" class="dropdown-item">Sign Up</b-link>
            <b-link to="/account/password-reset" class="dropdown-item">Forgot Password</b-link>
          </template>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-container>
  </b-navbar>
</template>

<script>
  export default {
    name: 'nav-header',
    data() {
      return {
        sideOpen: false
      }
    },
    computed: {
      user() {
        return this.$store.getters['session/user'];
      }
    },
    methods: {
      openSideBar() { // From what I gather, directly manipulating the DOM like this is bad,
        const root = document.getElementsByTagName('html')[0]; // But it's unavoidable because of the theme needing this
        this.sideOpen = !this.sideOpen;
        if (this.sideOpen) {
          root.setAttribute('class', 'nav-open');
        } else {
          root.removeAttribute('class', 'nav-open');
        }
      }
    }
  };
</script>

<style scoped>
</style>
