<template>
  <div class="wrapper">
    <div class="form-container">
      <div class="panel-heading">
        <h3 class="panel-title">Please sign in</h3>
      </div>
      <b-form v-if="!$store.state.authUser" @submit.prevent="login">
        <b-form-group id="exampleInputGroup1"
                      label="Your Name:" label-for="exampleInput1">
          <b-form-input id="exampleInput1"
                        v-model="formUsername"
                        type="text" required
                        placeholder="Enter name"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="exampleInputGroup2"
                      label="Password :" label-for="exampleInput2"
                      description="We'll never share your email with anyone else.">
          <b-form-input id="exampleInput2"
                        v-model="formPassword"
                        type="password" required
                        placeholder="Enter password"
          ></b-form-input>
        </b-form-group>

        <div class="link-container">
          <nuxt-link to="/register">Don't have an account ?</nuxt-link>
        </div>

        <b-form-group id="exampleGroup4">
          <b-form-checkbox id="exampleInput4">
            Remember me
          </b-form-checkbox>
        </b-form-group>


        <div class="button-container">
        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="secondary">Reset</b-button>
        </div>

      </b-form>
    </div>
  </div>
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
        this.$router.push('/home')
      } catch (e) {
        this.formError = e.message
      }
    },
    async logout () {
      try {
        await this.$store.dispatch('logout')
      } catch (e) {
        this.formError = e.message
      }
    }
  }
}
</script>

<style>
  .wrapper{
    height: 400px;
    background: white;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .form-container {
    width: 20%;
    height: 300px;
  }

  .button-container{
    display: flex;
    justify-content: space-between;
  }

  .link-container{
    margin-bottom: 10px;
  }

  .btn-primary{
    background-color: #17a2b8;
    border-color: #17a2b8;
  }

  .btn-primary:hover{
    background-color: #138496;
    border-color: #117a8b;
  }
</style>
