<template>
  <div>
    <div class="event-header">
      <span class="eyebrow">@{{ event.time }} on {{ event.date }}</span>
      <h1 class="title">{{ event.title }}</h1>
      <h5>Organized by {{ event.organizer ? event.organizer.name : '' }}</h5>
      <h5>Category: {{ event.category }}</h5>
    </div>
    <address>{{ event.location }}</address>
    <h2>Event details</h2>
    <p>{{ event.description }}</p>
    <h2>
      Attendees
      <span class="badge -fill-gradient">{{
        event.attendees ? event.attendees.length : 0
      }}</span>
    </h2>
    <ul class="list-group">
      <li
        v-for="(attendee, index) in event.attendees"
        class="list-item"
        :key="index"
      >
        <b>{{ attendee }}</b>
      </li>
    </ul>
  </div>
</template>

<script>
import EventService from '@/services/EventService.js'
import { mapState } from 'vuex'

export default {
  head() {
    return {
      title: 'Event #' + this.event.title
    }
  },
  props: ['id'],
  async fetch({ store, error, params }) {
    try {
      await store.dispatch('event/fetchEvent', params.id)
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event #' + params.id
      })
    }
  },
  computed: mapState({
    event: state => state.event.event
  })
}
</script>
