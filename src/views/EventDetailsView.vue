<script setup>
import { ref, onMounted } from 'vue'
import EventService from '../services/EventService.js'

import { computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const page = computed(() => parseInt(route.query.page) || 1)
console.log(page)

const props = defineProps({
    id: {
        required: true
    },
})

const event = ref(null)

onMounted(() => {
    EventService.getEvent(props.id).then((response) => {
        event.value = response.data
    }).catch((error) => {
        console.log(error)
    })
})
</script>

<template>
    <div v-if="event">
        <h1>{{ event.title }}</h1>
        <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
        <p>{{ event.description }}</p>

        <h1>You are on page {{ $route.params }}</h1>

  </div>
</template>

<style scoped></style>