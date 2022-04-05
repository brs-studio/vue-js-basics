<template>
  <div>
    <div class="event-header">
      <h1 class="title">
        {{ event.title }}
      </h1>
      <span class="eyebrow">
        @{{ event.time }} on {{ event.date }}
        <span class="badge -fill-gradient">
          Attendees {{ event.attendees ? event.attendees.length : 0 }}
        </span></span
      >
      <span name="map" class="map">
        <div class="flex">
          <h2>Category:</h2>
          <h5 class="content">{{ event.category }}</h5>
        </div>
      </span>
    </div>

    <span name="map" class="map">
      <div class="flex">
        <h2>Location:</h2>
        <h5 class="content">{{ event.location }}</h5>
      </div>
    </span>

    <h2>Event details</h2>
    <p>{{ event.description }}</p>
    <h2>
      <h5>
        Organized by<span class="organ">
          {{ event.organizer ? event.organizer.name : '' }}</span
        >
      </h5>
      <br />
    </h2>
    <ul class="list-group">
      <li
        v-for="(attendee, index) in event.attendees"
        :key="index"
        class="list-item"
      >
        <b>{{ attendee.name }}</b>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  async fetch({ store, error, params }) {
    try {
      await store.dispatch('events/fetchEvent', params.id)
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event #' + params.id,
      })
    }
  },
  computed: mapState({
    event: (state) => state.events.event,
  }),
  head() {
    return {
      title: 'Event #' + this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about  #' + this.event.title,
        },
      ],
    }
  },
}
</script>

<style scoped>
.prompt-box {
  position: relative;
  overflow: hidden;
  padding: 1em;
  margin-bottom: 24px;
  transform: scaleY(1);
}
.prompt-box > .title {
  margin: 0 0 0.5em;
}
.prompt-box > .title > .meta {
  margin-left: 10px;
}
.prompt-box > .actions {
  display: flex;
  align-items: center;
}
.prompt-box > button {
  margin-right: 0.5em;
}
.prompt-box > button:last-of-type {
  margin-right: 0;
}
.location {
  margin-bottom: 0;
}
.location > .icon {
  margin-left: 10px;
}
.event-header > .title {
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
h1 {
  font-size: 2vw;
  font-weight: 400;
}
span.eyebrow {
  font-size: 0.9vw;
  font-weight: 400;
  color: grey;
}
h5 {
  font-size: 1.5vw;
  font-weight: 300;
}
h2 {
  font-size: 2vw;
  font-weight: 300;
}
span.map h2 {
  font-size: 2vw;
  font-weight: 400;
}
span.badge.-fill-gradient {
  margin-left: 90px;
}
span.content {
  font-size: 25px;
  font-weight: normal;
}
div.flex {
  display: flex;
}
</style>
