<template>
  <div>
    <h2 v-if="vehicleswaiting.length > 0">Vehicles Waiting List:</h2>
    <v-row>
      <v-col v-bind:key="vehiclewaiting.id" v-for="vehiclewaiting in vehicleswaiting" :cols="1">
        <VehicleWaiting v-bind:vehiclewaiting="vehiclewaiting" />
      </v-col>
    </v-row>
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