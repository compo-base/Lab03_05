<script setup lang="ts">
import type { PassengerInfo } from '@/type'
import { computed, ref, watchEffect } from 'vue'
import type { Ref } from 'vue'
import PassengerService from '@/services/PassengerService'
import PassengerCard from '@/components/PassengerCard.vue'
import type { Axios, AxiosResponse } from 'axios'
const passengers: Ref<Array<PassengerInfo>> = ref([])
// const eventsPerPage = ref(2)
const totalEvent = ref<number>(0)
const props = defineProps({
  page: {
    type: Number,
    required: true
  }
})

watchEffect(() => {
  PassengerService.getEvent(5, props.page).then((response: AxiosResponse<PassengerInfo[]>) => {
    passengers.value = response.data
    totalEvent.value = response.headers['x-total-count']
  })
})
const hasNextPages = computed(() => {
  const totalPages = Math.ceil(totalEvent.value / 5)
  return props.page.valueOf() < totalPages
})
</script>

<template>
  <main class="container">
    <PassengerCard
      v-for="passenger in passengers"
      :key="passenger.id"
      :passenger="passenger"
    ></PassengerCard>
    <div class="pagination">
      <RouterLink
        :to="{ name: 'passenger', query: { page: page - 1 } }"
        rel="prev"
        v-if="page != 1"
        id="page-prev"
      >
        Prev page
      </RouterLink>
      <RouterLink
        :to="{ name: 'passenger', query: { page: page + 1 } }"
        rel="next"
        v-if="hasNextPages"
        id="page-next"
      >
        Next page
      </RouterLink>
    </div>
  </main>
</template>
