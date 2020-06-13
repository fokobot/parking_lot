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
      ],
      smallspaces: 0,
      mediumspaces: 0
    }
  },
  methods: {
    addVehicle(newVehicle) {
      if (!this.canIPark(newVehicle.type)) this.vehicleswaiting = [...this.vehicleswaiting, newVehicle];
    },
    freeUpParking(id) {
      let index = this.parkingspaces.findIndex(parkingspace => parkingspace.id === id);
      this.parkingspaces[index].status = false;
      this.updateSpaces(this.parkingspaces[index].type);
      return this.vehicleswaiting.some(vehicle => {
        if (this.canIPark(vehicle.type)) {
          this.vehicleswaiting = this.vehicleswaiting.filter(waiting => waiting.id !== vehicle.id);
          return true;
        }
        return false;
      })
    },
    canIParkHere(vehicleType, parkingspace) {
      let canPark = false;
      if (!parkingspace.status) {
        switch (vehicleType) {
          case 'Motorcycle':
            if (this.smallspaces > 0) {
              if (parkingspace.type === size.SMALL) {
                canPark = true;
                this.smallspaces--;
              }
            } else {
              if (this.mediumspaces > 0) {
                if (parkingspace.type === size.MEDIUM) {
                  canPark = true;
                  this.mediumspaces--;
                }
              } else {
                canPark = true;
              }
            }
            break;
          case 'Sedan':
            if (parkingspace.type !== size.SMALL) {
              if (this.mediumspaces > 0) {
                if (parkingspace.type === size.MEDIUM) {
                  canPark = true;
                  this.mediumspaces--;
                }
              } else {
                canPark = true;
              }
            }
            break;
          case 'Truck':
            if (parkingspace.type === size.LARGE) {
              canPark = true;
            }
            break;
          default:
            console.log('Vehicle type doesn\'t exist');
            break;
        }
      }
      if (canPark) {
        parkingspace.status = true;
      }
      return canPark;
    },
    canIPark(vehicleType) {
      return this.parkingspaces.some(parkingspace => {
        if (this.canIParkHere(vehicleType, parkingspace)) return true;
      });
    },
    updateSpaces(type) {
      switch (type) {
        case 'Small':
          this.smallspaces++;
          break;
        case 'Medium':
          this.mediumspaces++;
          break;
      }
    }
  },
  created() {
    this.parkingspaces.forEach(parkingspace => {
      this.updateSpaces(parkingspace.type);
    })

  }
}
</script>
