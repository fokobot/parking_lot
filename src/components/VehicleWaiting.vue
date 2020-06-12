<template>
  <div>
    <v-icon large v-if="vehiclewaiting.type === 'Motorcycle'">directions_bike</v-icon>
    <v-icon large v-else-if="vehiclewaiting.type === 'Sedan'">directions_car</v-icon>
    <v-icon large v-else>local_shipping</v-icon>
  </div>
</template>

<script>
export default {
  name: 'VehicleWaiting',
  props: ['vehiclewaiting'],
  methods: {

  }
}
</script>