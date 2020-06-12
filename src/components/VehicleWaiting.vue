<template>
  <div>
    <h3>I am a vehicle waiting {{ vehiclewaiting.type }}</h3>
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