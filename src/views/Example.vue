<template>
  <div>
    <input 
      type="email"
      placeholder="What's your email"
      v-model.trim="email"
      @blur="$v.email.$touch()"
      :class="{ error: $v.email.$error }"
    />
    <div v-if="$v.email.$error">
      <p class="errorMessage" v-if="!$v.email.email">
        Please enter a valid email address.
      </p>
      <p class="errorMessage" v-if="!$v.email.required">
        Email is required.
      </p>
    </div>
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
