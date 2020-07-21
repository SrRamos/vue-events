<template>
  <div>
    <div class="event-header">
      <span class="eyebrow">@{{ event.time }} on {{ event.date | date }}</span>
      <span class="title">{{ event.title }}</span>
      <span>Organized by {{ event.organizer ? event.organizer.name : '' }}</span>
      <span>Category: {{ event.category }}</span>
    </div>

    <BaseIcon class="location" name="map">
      <h2>Location</h2>
    </BaseIcon>

    <span>{{ event.location }}</span>

    <h2>Event details</h2>
    <p>{{ event.description }}</p>

    <h2>
      Attendees
      <span class="badge -fill-gradient">{{ event.attendees ? event.attendees.length : 0 }}</span>
    </h2>
    <ul class="list-group">
      <li v-for="(attendee, index) in event.attendees" :key="index" class="list-item">
        <b>{{ attendee.name }}</b>
      </li>
    </ul>

    <BaseButton @click="deleteEvent" type="button" buttonClass="-fill-gradient">Remove Event</BaseButton>
  </div>
</template>
<script>
import NProgress from 'nprogress'
import BaseIcon from '@/components/BaseComponents/BaseIcon.vue'
import date from '@/filters/date'
import BaseButton from '@/components/BaseComponents/BaseButton.vue'

export default {
  props: ['event'],
  components: {
    BaseIcon,
    BaseButton
  },
  filters: {
    date
  },
  methods: {
    deleteEvent() {
      NProgress.start()
      this.$store
        .dispatch('event/removeEvent', this.event)
        .then(() => {
          this.event = this.createFreshEventObject()
          this.$router.push({
            path: '/'
          })
        })
        .catch(() => {
          NProgress.done()
        })
    }
  }
}
</script>
<style scoped>
.location {
  margin-bottom: 0;
}
.location > .icon {
  margin-left: 10px;
}
.title {
  margin: 0;
}
.list-group {
  margin: 0;
  padding: 0;
  list-style: none;
}
.list-group > .list-item {
  padding: 1em 0;
  border-bottom: solid 1px #e5e5e5;
}
</style>
