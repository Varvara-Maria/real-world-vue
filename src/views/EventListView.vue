<script setup>
import EventCard from "@/components/EventCard.vue";
import EventService from "@/services/EventService.js";
import {onBeforeMount, ref,} from "vue";

const events = ref(null)


onBeforeMount(() => {
  EventService.getEvents()
      .then((response) => {
        events.value = response.data
      })
      .catch((error) => {
        console.log(error)
      })
});

</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <div>
      <EventCard v-for="event in events" :key="event.id" :event="event" />
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
