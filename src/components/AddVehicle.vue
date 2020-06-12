<template>
  <div>
    <v-form ref="form">
      <v-row>
        <v-col cols="8">
          <v-select
            v-model="vehicle"
            :items="items"
            :rules="[v => !!v || 'Item is required']"
            label="Vehicle"
            required
          ></v-select>
        </v-col>
        <v-col cols="4">
          <v-btn :disabled="!valid" @click="validate" class="mr-4">Agregar Vehiculo</v-btn>
        </v-col>
      </v-row>
    </v-form>
  </div>
</template>

<script>
import { v4 as uuid } from 'uuid';
export default {
  name: "AddTodo",
  data() {
    return {
      valid: true,
      vehicle: null,
      items: [
        'Motorcycle',
        'Sedan',
        'Truck'
      ],
    }
  },
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        this.addVehicle();
      }
    },
    addVehicle() {
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