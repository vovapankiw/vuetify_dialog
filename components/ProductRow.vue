<template>
  <div>
    <v-layout align-center justify-center>
      <v-flex xs12 sm6 md4 text-xs-center>
        <span>{{ product.title }}</span>
      </v-flex>
      <v-flex xs12 sm6 md2 text-xs-center>
        <span> {{ selectedPrice }}</span>
      </v-flex>
      <v-flex xs12 sm6 md3 text-xs-center>
        <v-select
          v-model="selectedPrice"
          :items="product.measurement"
          item-text="height"
          item-value="price"
          label="Select"
          persistent-hint
          single-line
          attach
        >
        </v-select>
      </v-flex>
      <v-flex xs12 sm6 md2 text-xs-center>
        <v-edit-dialog
            @open="product.quantity = product.quantity;"
            @cancel="product.quantity = product.quantity"
          > {{ product.quantity }}
            <v-text-field
              slot="input"
              label="Edit"
              :value="product.quantity"
              @change="changeQuantity($event,product.id)"
              single-line counter="counter"
              ref="test"
            ></v-text-field>
          </v-edit-dialog>
      </v-flex>
      <v-flex xs12 sm6 md1 text-xs-center>
         <v-btn flat icon color="red lighten-2">
          <v-icon>delete</v-icon>
        </v-btn>
      </v-flex>
    </v-layout>
    <v-divider />
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      selectedPrice: this.product.measurement[0].price,
    }
  },
  methods: {
    changeQuantity(quantity, id) {
      this.$emit('change', {quantity, id} )
    }
  },
}
</script>


<style>
  .v-select {
    justify-content: center;
  }

  .v-select .v-input__control {
    max-width: 80%;
  }
</style>

