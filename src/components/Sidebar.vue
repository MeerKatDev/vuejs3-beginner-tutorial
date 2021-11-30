<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <button class="cart-close" @click="toggle">&times;</button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(quantity, name, i) in cart" :key="i">
              <td><i class="icofont-{{ getIcon(name) }} icofont-3x"></i></td>
              <td>{{ name }}</td>
              <td>${{ getPrice(name) }}</td>
              <td class="center">{{ quantity }}</td>
              <td>${{ quantity * getPrice(name) }}</td>
              <td class="center">
                <button @click="remove(name)" class="btn btn-light cart-remove" >
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p class="center" v-if="Object.keys(cart).length == 0"><em>No items in cart</em></p>
        <div class="spread">
          <span><strong>Total:</strong> ${{ calculateTotal }} </span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: ['toggle', 'cart', 'inventory', 'remove'],
  computed: {
    calculateTotal () {
      return Object.entries(this.cart).reduce((acc, [key, quantity]) => {
        return acc + (quantity * this.getPrice(key))
      }, 0).toFixed(2)
    }
  },
  methods: {
    getProduct (name) {
      return this.inventory.find(p => p.name === name)
    },
    getIcon (name) {
      return this.getProduct(name).icon
    },
    getPrice (name) {
      return this.getProduct(name).price.USD
    }
  }
}
</script>
