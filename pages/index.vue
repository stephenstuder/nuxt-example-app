<template>
  <div>
    <h1>Events</h1>
    <EventCard
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
  async asyncData({ $axios, error }) {
    await $axios
      .get('http://localhost:3000/events')
      .then((response) => {
        return {
          events: response.data,
        }
      })
      .catch((e) => {
        error({
          statusCode: 503,
          message: 'Opps, We Bonked. Please Try Again.',
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
