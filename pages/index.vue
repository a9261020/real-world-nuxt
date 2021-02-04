<template>
  <div>
    <h1>Events</h1>
    <event-card
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '~/components/EventCard.vue'

export default {
  components: { EventCard },
  asyncData({ $axios, error }) {
    return $axios
      .get('http://localhost:3000/events')
      .then((res) => {
        return {
          events: res.data,
        }
      })
      .catch(() => {
        error({
          statusCode: 503,
          message: 'Unable to fetch events at this time. Please try again',
        })
      })
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
}
</script>
