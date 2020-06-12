<template>
  <div>
    <v-responsive>
      <v-card
        class="mx-auto"
        v-bind:class="parkingspace.status ? 'green' : 'red'"
        dark
        max-width="400"
      >
        <v-card-title>
          <v-icon large left>aspect_ratio</v-icon>
          <span class="title font-weight-light">{{ parkingspace.type }}</span>
        </v-card-title>

        <v-card-actions>
          <v-list-item class="grow">
            <v-row>
              <v-btn
                @click="$emit('free-up',parkingspace.id)"
                :disabled="!parkingspace.status"
                color="primary"
              >Free Up Parking Space</v-btn>
            </v-row>
            <v-row align="center" justify="end">
              <div>
                <v-icon class="mr-1">directions_bike</v-icon>
                <span class="mr-1"></span>
              </div>
              <div v-if="parkingspace.type === 'Large' || parkingspace.type === 'Medium'">
                <v-icon class="mr-1">directions_car</v-icon>
                <span class="mr-1"></span>
              </div>
              <v-icon v-if="parkingspace.type === 'Large'" class="mr-1">local_shipping</v-icon>
            </v-row>
          </v-list-item>
        </v-card-actions>
      </v-card>
    </v-responsive>
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