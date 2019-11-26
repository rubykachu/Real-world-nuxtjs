<template>
  <div>
    <h1>Events List</h1>
    <!-- <EventCard v-for="event in events" :key="event.id" :event="event" /> -->
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'
import { mapState } from 'vuex'

export default {
  components: {
    EventCard
  },
  head() {
    return {
      title: 'Event Listing'
    }
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('event/fetchEvents')
    } catch (e) {
      error({
        statusCode: 404,
        message: 'Unable to fetch events'
      })
    }
  },
  computed: mapState({
    events: state => state.event.events
  })
}
</script>
