<template>
  <div>
    <input type="email" placeholder="What's your email" v-model="email"/>
    <button type="submit">Submit</button>
  </div>
</template>

<script>
import { required, email } from 'vuelidate/lib/validators'

export default {
  data() {
    return {
      email: null
    }
  },
  validations: {
    email: {
      required,
      email
    }
  }
}
</script>
