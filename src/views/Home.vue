<template>
  <div class="home">
    <v-container>
      <AddVehicle v-on:add-vehicle="addVehicle" />
      <VehicleWaitingList v-bind:vehicleswaiting="vehicleswaiting" />
      <ParkingSpaceList v-bind:parkingspaces="parkingspaces" v-on:free-up="freeUpParking" />
    </v-container>
  </div>
</template>

<script>
import ParkingSpaceList from '../components/ParkingSpaceList'
import VehicleWaitingList from '../components/VehicleWaitingList'
import AddVehicle from '../components/AddVehicle'

const size = {
  SMALL: 'Small',
  MEDIUM: 'Medium',
  LARGE: 'Large'
}
export default {

  name: 'Home',
  components: {
    ParkingSpaceList,
    VehicleWaitingList,
    AddVehicle
  },
  data() {
    return {
      parkingspaces: [
        {
          id: 1,
          type: size.SMALL,
          status: false
        },
        {
          id: 2,
          type: size.LARGE,
          status: false
        },
        {
          id: 3,
          type: size.MEDIUM,
          status: false
        },
        {
          id: 4,
          type: size.MEDIUM,
          status: false
        },
        {
          id: 5,
          type: size.LARGE,
          status: false
        },
        {
          id: 6,
          type: size.LARGE,
          status: false
        },
        {
          id: 7,
          type: size.MEDIUM,
          status: false
        },
        {
          id: 8,
          type: size.SMALL,
          status: false
        }
      ],
      vehicleswaiting: [
      ]
    }
  },
  methods: {
    addVehicle(newVehicle) {
      if (!this.canIPark(newVehicle.type)) this.vehicleswaiting = [...this.vehicleswaiting, newVehicle];
    },
    freeUpParking(id) {
      let index = this.parkingspaces.findIndex(parkingspace => parkingspace.id === id);
      this.parkingspaces[index].status = false;
      return this.vehicleswaiting.some(vehicle => {
        if (this.canIPark(vehicle.type)) {
          this.vehicleswaiting = this.vehicleswaiting.filter(waiting => waiting.id !== vehicle.id);
          return true;
        } else {
          return false;
        }
      })
    },
    canIParkHere(vehicleType, parkingspace) {
      switch (vehicleType) {
        case 'Motorcycle':
          if (!parkingspace.status) {
            parkingspace.status = true;
            return true;
          } else {
            return false;
          }
        case 'Sedan':
          if (!parkingspace.status && parkingspace.type !== size.SMALL) {
            parkingspace.status = true;
            return true;
          } else {
            return false;
          }
        case 'Truck':
          if (!parkingspace.status && parkingspace.type !== size.SMALL && parkingspace.type !== size.MEDIUM) {
            parkingspace.status = true;
            return true;
          } else {
            return false;
          }
        default:
          console.log('Vehicle type doesn\'t exist');
          return false;
      }
    },
    canIPark(vehicleType) {
      return this.parkingspaces.some(parkingspace => {
        if (this.canIParkHere(vehicleType, parkingspace)) return true;
      });
    }
  }
}
</script>
