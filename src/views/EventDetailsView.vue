<script setup>
import {onBeforeMount, ref} from "vue";
import EventService from "@/services/EventService";

const event = ref(null);
const props = defineProps({
  id: {
    required: true,
  }
})
onBeforeMount(() => {
  EventService.getEvent(props.id)
      .then((response) => {
        event.value = response.data
      })
      .catch((error) => {
        console.log(error)
      })
})

</script>

<template>
  <div v-if="event">
    <h2>{{ event.title }}</h2>
    <span>@{{ event.time}} on {{ event.date }} @ {{ event.location }}</span>
    <p>{{ event.description }}</p>
  </div>
</template>