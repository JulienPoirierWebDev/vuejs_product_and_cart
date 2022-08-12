<template>
  <aside className="cart-container">
    <div className="cart">
      <h1 className="cart-title spread">
        <span>
        Cart
        <i className="icofont-cart-alt icofont-1x"> </i>
      </span>
        <button @click="toggle" className="cart-close">&times;</button>
      </h1>

      <div className="cart-body">
        <table className="cart-table">
          <thead>
          <tr>
            <th><span className="sr-only">Product Image</span></th>
            <th>Product</th>
            <th>Price</th>
            <th>Qty</th>
            <th>Total</th>
            <th><span className="sr-only">Actions</span></th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(quantity, key, i) in cart" :key="i" >
            <td><i className="icofont-carrot icofont-3x"></i></td>
            <td>{{ key }}</td>
            <td>${{ getPrice(key) }}</td>
            <td className="center">{{ quantity }}</td>
            <td>${{ (quantity * getPrice(key)).toFixed(2) }}</td>
            <td className="center">
              <button @click="remove(key)" className="btn btn-light cart-remove">
                &times;
              </button>
            </td>
          </tr>

          </tbody>
        </table>

        <p className="center" v-if="cart && !Object.keys(cart).length"><em>No items in cart</em></p>
        <div className="spread">
          <span v-if="Object.keys(cart).length"><strong>Total:</strong>${{calculateTotal()}}</span>
          <button className="btn btn-light" v-if="Object.keys(cart).length">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'SidebarCart',
  props: ['toggle', 'cart', 'inventory', 'remove'],
  methods: {
    getPrice (name) {
      const product = this.inventory.find((p) => {
        return p.name === name
      })
      return (product.price.USD).toFixed(2)
    },
    calculateTotal () {
      const total = Object.entries(this.cart).reduce(
        (acc, curr, index) => {
          return acc + (curr[1] * this.getPrice(curr[0]))
        }, 0)
      return total.toFixed(2)
    }
  }

}
</script>

<style scoped>

</style>
