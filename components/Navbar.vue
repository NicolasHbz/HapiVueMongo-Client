<template>
  <b-navbar toggleable="md" type="dark" variant="dark">

    <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

    <b-navbar-brand @click="logout" id="logo">HapiVueMongo</b-navbar-brand>

    <b-collapse is-nav id="nav_collapse">


      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">

        <b-nav-form>
          <b-form-input size="sm" class="mr-sm-2" type="text" placeholder="Search"
                        v-if="$store.state.authUser && $store.state.authUser.username"
          />
          <b-button size="sm" class="my-2 my-sm-0" type="submit" v-if="$store.state.authUser && $store.state.authUser.username">
            Search
          </b-button>
        </b-nav-form>

        <Nuxt />

        <b-nav-item-dropdown right v-if="$store.state.authUser && $store.state.authUser.username">
          <!-- Using button-content slot -->
          <template slot="button-content">
            <em >{{ $store.state.authUser.username }}</em>
          </template>
          <b-dropdown-item href="#">Profile</b-dropdown-item>
          <b-dropdown-item @click="logout">Signout</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>

    </b-collapse>
  </b-navbar>
</template>

<script>
export default {
  data () {
    return {
      formError: null,
      formUsername: '',
      formPassword: ''
    }
  },
  methods: {
    async login () {
      try {
        await this.$store.dispatch('login', {
          username: this.formUsername,
          password: this.formPassword
        })
        this.formUsername = ''
        this.formPassword = ''
        this.formError = null
      } catch (e) {
        this.formError = e.message
      }
    },
    async logout () {
      try {
        await this.$store.dispatch('logout')
        this.$router.push('/')
      } catch (e) {
        this.formError = e.message
      }
    }
  }
}
</script>

<style>
  #logo:hover{
    cursor: pointer;
  }
</style>
