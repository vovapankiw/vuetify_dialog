<template>
    <div id="app">
      <v-layout row justify-center>
        <v-dialog v-model="dialog" persistent max-width="600px">
          <template v-slot:activator="{ on }">
            <v-btn color="primary" dark v-on="on">Open Dialog</v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">Корзина</span>
            </v-card-title>
            <v-card-text>
              <v-container grid-list-md>
                <v-layout wrap align-center justify-center>
                  <v-flex xs12 sm6 md4 text-xs-center>
                    <span class="subheading">Назва</span>
                  </v-flex>
                  <v-flex xs12 sm6 md2 text-xs-center>
                    <span class="subheading">Ціна</span>
                  </v-flex>
                  <v-flex xs12 sm6 md3 text-xs-center>
                    <span class="subheading">Висота</span>
                  </v-flex>
                  <v-flex xs12 sm6 md2 text-xs-center>
                    <span class="subheading">Кількість</span>
                  </v-flex>
                  <v-flex xs12 sm6 md1 text-xs-center>
                  </v-flex>
                </v-layout>
                <v-divider />
                <ProductRow
                  v-for="product in products"
                  :key="product.id"
                  :product="product"
                  @change="setProductQuantity"
                /> 
                <v-flex>
                  <span> {{ totalQuantity }}</span>
                </v-flex> 
                <v-layout wrap align-center justify-center>
                  <v-flex xs12 sm6 md4>
                    <v-text-field label="Legal first name*" required></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field label="Legal middle name" hint="example of helper text only on focus"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field
                      label="Legal last name*"
                      hint="example of persistent helper text"
                      persistent-hint
                      required
                    ></v-text-field>
                  </v-flex>
                  <v-flex xs12>
                    <v-text-field label="Email*" required></v-text-field>
                  </v-flex>
                  <v-flex xs12>
                    <v-text-field label="Password*" type="password" required></v-text-field>
                  </v-flex>
                </v-layout>
              </v-container>
              <small>*indicates required field</small>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" flat @click="dialog = false">Close</v-btn>
              <v-btn color="blue darken-1" flat @click="dialog = false">Save</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-layout>
  </div>
</template>

<script>
import ProductRow from '~/components/ProductRow';

export default {
  components: {
    ProductRow,
  },
  data() {
    return {
      dialog: false,
      products: [
        {
          id: 1,
          title: 'Ялина',
          measurement: [{height: '120-150', price: 50}, {height: '150-180', price: 80}],
          quantity: 10,
        },
        {
          id: 2,
          title: 'Сосна',
          measurement: [{height: '120-150', price: 50}, {height: '150-180', price: 80}],
          quantity: 5,
        }
      ]
    }
  },
  computed: {
    totalQuantity() {
      return this.products.reduce((prev, el) => prev + parseInt(el.quantity),0)
    }
  },
  methods: {
    setProductQuantity(data) {
      const index = this.products.findIndex(el => el.id === data.id);
      this.products[index].quantity = data.quantity;
    }
  }
}
</script>
