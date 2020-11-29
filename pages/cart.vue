<template>
  <div>
    <h2>Your Cart</h2>
    <hr>
    <div v-for="product in getCart" :key="product._id">
      <h2>{{product.title}}</h2>
      <h3>Qty: {{product.quantity}}</h3>
      <h3>$ {{product.price * product.quantity}}</h3>
      <!-- <div>{{product.rating}}</div> -->
      <img src="/impact-whey-protein.jpg"/>
      <button @click="$store.commit('removeProduct', product)">Remove</button>
      <div>
          <h3>Description:</h3>
          <p>{{product.description}}</p>
      </div>
    </div>
    <hr>
    <h3>Subtotal({{getCartLength}} items): ${{getCartTotalPrice}}</h3>
    <button>Proceed to Checkout</button>
  </div>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
  computed: {
    ...mapGetters(["getCart", "getCartTotalPrice", "getCartLength"])
  }
}
</script>
