<template>
  <div>
    <form @submit="addVehicle">
      <select v-model="vehicle">
        <option disabled value>Seleccione un elemento</option>
        <option>Motorcycle</option>
        <option>Sedan</option>
        <option>Truck</option>
      </select>
      <input type="submit" value="Agregar Vehiculo" class="btn" />
    </form>
  </div>
</template>

<script>
import { v4 as uuid } from 'uuid';
export default {
  name: "AddTodo",
  data() {
    return {
      vehicle: ''
    }
  },
  methods: {
    addVehicle(e) {
      e.preventDefault();
      const newVehicle = {
        id: uuid(),
        type: this.vehicle
      }
      // Send up to parent
      this.$emit('add-vehicle', newVehicle)
    }
  }
}
</script>