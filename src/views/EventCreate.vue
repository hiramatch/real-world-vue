<template>
  <div>
    <h1>Create an Event</h1>
    <form @submit.prevent="createEvent">
      <BaseSelect
        label="Select a category"
        v-model="event.category"
        :options="categories"
        :class="{ error: $v.event.category.$error}"
        @blur="$v.event.category.$touch()"
      />
      <template v-if="$v.event.category.$error">
      <p v-if="!$v.event.category.required" class="errorMessage">Category is required.</p>
     </template>

      <h3>Name & describe your event</h3>
      <BaseInput
        label="Title"
        v-model="event.title"
        type="text"
        placeholder="Add an event title"
        :class="{ error: $v.event.title.$error}"
        @blur="$v.event.title.$touch()"
      />
      <template v-if="$v.event.title.$error">
      <p v-if="!$v.event.title.required" class="errorMessage">Title is required.</p>
     </template>

      <BaseInput
        label="Description"
        v-model="event.description"
        type="text"
        placeholder="Add a description"
        :class="{ error: $v.event.description.$error}"
        @blur="$v.event.description.$touch()"
      />
      <template v-if="$v.event.description.$error">
      <p v-if="!$v.event.description.required" class="errorMessage">Description is required.</p>
     </template>

      <h3>Where is your event?</h3>
      <BaseInput
        label="Location"
        v-model="event.location"
        type="text"
        placeholder="Add a location"
        :class="{ error: $v.event.location.$error}"
        @blur="$v.event.location.$touch()"
      />
      <template v-if="$v.event.location.$error">
      <p v-if="!$v.event.location.required" class="errorMessage">Location is required.</p>
     </template>

      <h3>When is your event?</h3>

      <div class="field">
        <label>Date</label>
        <datepicker v-model="event.date" placeholder="Select a date"/>
      </div>

      <BaseSelect
        label="Select a time"
        v-model="event.time"
        :options="times"
        class="field"
      />
      <BaseButton type="submit" buttonClass="-fill-gradient">Submit</BaseButton>
    </form>
  </div>
</template>


<script>
import Datepicker from 'vuejs-datepicker'
import NProgress from 'nprogress'
import { required } from 'vuelidate/lib/validators'

export default {
  components: {
    Datepicker
  },
  data() {
    const times = []
    for (let i = 1; i <= 24; i++) {
      times.push(i + ':00')
    }
    return {
      times,
      categories: this.$store.state.categories,
      event: this.createFreshEventObject()
    }
  },
  methods: {
    createEvent() {
      NProgress.start()
      this.$store
        .dispatch('event/createEvent', this.event)
        .then(() => {
          this.$router.push({
            name: 'event-show',
            params: { id: this.event.id }
          })
          this.event = this.createFreshEventObject()
        })
        .catch(() => {
          NProgress.done()
        })
    },
    createFreshEventObject() {
      const user = this.$store.state.user.user
      const id = Math.floor(Math.random() * 10000000)

      return {
        id: id,
        user: user,
        category: '',
        organizer: user,
        title: '',
        description: '',
        location: '',
        date: '',
        time: '',
        attendees: []
      }
    }
  },
  validations: {
    event: {
      category: { required },
      title: { required },
      description: { required },
      location: { required },
      date: { required },
      time: { required }
    }
  }
}
</script>

<style scoped>
.field {
  margin-bottom: 24px;
}
</style>
