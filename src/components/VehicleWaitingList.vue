<template>
  <div>
    <div v-bind:key="vehiclewaiting.id" v-for="vehiclewaiting in vehicleswaiting">
      <VehicleWaiting v-bind:vehiclewaiting="vehiclewaiting" />
    </div>
  </div>
</template>

<script>
import VehicleWaiting from './VehicleWaiting'

export default {
  name: 'VehicleWaitingList',
  components: {
    VehicleWaiting
  },
  props: ['vehicleswaiting']
}
</script>