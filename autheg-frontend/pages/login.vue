<template lang="pug">
v-layout
  v-flex
    v-card(v-if='$auth.state.loggedIn')
      v-alert(type='error', :value='error') {{error}}
      v-card-text
        | Logged in as {{$auth.state.user.email}}
      v-card-actions
        v-btn(@click='logout') Log out
    v-card(v-else='')
      v-alert(type='error', :value='error') {{error}}
      v-card-text
        v-form
          v-text-field(v-model='email', label='Email')
          v-text-field(v-model='password', label='Password', type='password')
        v-card-actions
          v-btn(@click='login') Log in
</template>

<script>
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    login: function () {
      this.$auth.login({
        data: {
          user: {
            email: this.email,
            password: this.password
          }
        }
      }).catch(e => {this.error = e + ''})
    },
    logout: function () {
      this.$auth.logout().catch(e => {this.error = e + ''})
    }
  }
}
</script>
