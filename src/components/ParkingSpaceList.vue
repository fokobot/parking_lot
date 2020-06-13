<template>
  <div>
    <v-container>
      <v-row :flex="6">
        <v-col v-bind:key="parkingspace.id" v-for="parkingspace in parkingspaces">
          <ParkingSpace
            v-bind:parkingspace="parkingspace"
            v-on:free-up="$emit('free-up', parkingspace.id)"
          />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import ParkingSpace from './ParkingSpace'

export default {
  name: 'ParkingSpaceList',
  components: {
    ParkingSpace
  },
  props: ['parkingspaces']
}
</script>