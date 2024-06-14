<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script setup>
import EventService from '@/services/EventService'
import { ref, onMounted } from 'vue'

const event = ref(null)

const props = defineProps({
  id: {
    required: true
  }
})

onMounted(() => {
  //fetch event by id  and set local data

  EventService.getEvent(props.id)
    .then((res) => {
      event.value = res.data
    })
    .catch((error) => {
      console.log(error)
    })
})
</script>

<style lang="scss" scoped></style>
