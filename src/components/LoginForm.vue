<template>
  <v-container fill-height>
    <v-row align="center" justify="center">
      <v-col>
        <v-card class="mx-auto my-auto" max-width="344" outlined fill-height fluid>
          <form>
            <v-text-field v-model="password" :error-messages="passwordErrors" label="Password" required type="password"
              @input="$v.password.$touch()" @blur="$v.password.$touch()"></v-text-field>
            <v-text-field v-model="email" :error-messages="emailErrors" label="E-mail" required
              @input="$v.email.$touch()" @blur="$v.email.$touch()"></v-text-field>

            <v-btn class="mr-4" @click="submit">
              submit
            </v-btn>
            <v-btn @click="clear">
              clear
            </v-btn>
          </form>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>

import { validationMixin } from 'vuelidate'
import { required, email, minLength } from 'vuelidate/lib/validators'
export default {
  name: 'LoginForm',
  mixins: [validationMixin],
  validations: {
    email: { required, email },
    password: {
      required,
      minLength: minLength(6)
    },
  },
  data: () => ({
    password: '',
    email: '',
  }),
  computed: {
    passwordErrors() {
      const errors = []
      if (!this.$v.password.$dirty) return errors
      !this.$v.password.minLength && errors.push('password must be at at least 6 characters long')
      !this.$v.password.required && errors.push('Password is required.')
      return errors
    },
    emailErrors() {
      const errors = []
      if (!this.$v.email.$dirty) return errors
      !this.$v.email.email && errors.push('Must be valid e-mail')
      !this.$v.email.required && errors.push('E-mail is required')
      return errors
    },
  },
  methods: {
    submit() {
      this.$v.$touch()
    },
    clear() {
      this.$v.$reset()
      this.password = ''
      this.email = ''
    },
  },
}
</script>


