<template>
  <router-link class="event-link" :to="{ name: 'event-show', params: { id: event.id } }">
    <div class="event-card -shadow">
      <span :class="'eyebrow'">@{{ event.time }} on {{ event.date | date }}</span>
      <h4 class="title">{{ event.title }}</h4>
      <BaseIcon name="users">{{ event.attendees.length }} attending</BaseIcon>
    </div>
  </router-link>
</template>

<script>
import DateFilter from '@/filters/date'

export default {
  props: {
    event: Object
  },
  filters: {
    'date': DateFilter
  }
}
</script>

<style module>
.event-card {
  padding: 20px;
  margin-bottom: 24px;
  cursor: pointer;
}
.event-card > .title {
  margin: 0;
}
.event-link {
  color: black;
  text-decoration: none;
  font-weight: 100;
}
</style>
