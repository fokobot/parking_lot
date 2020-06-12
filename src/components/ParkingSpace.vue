<template>
  <div>
    <h3>I am a parking space {{ parkingspace.type }}</h3>
    <button
      @click="$emit('free-up',parkingspace.id)" :disabled="!parkingspace.status"
    >Free Up Parking Space</button>
  </div>
</template>

<script>
export default {
  name: 'ParkingSpace',
  props: ['parkingspace'],
  methods: {

  }
}
</script>