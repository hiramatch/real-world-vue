<template>
  <div>
    <h1>Events Listing</h1>
    <router-link class="event-link" :to="{ name: 'event-show', params: { id: '1' } }">
      <event-card/>
    </router-link>
  </div>
</template>
<script>
import EventCard from '@/components/EventCard.vue'

export default {
  components: {
    EventCard
  }
}
</script>