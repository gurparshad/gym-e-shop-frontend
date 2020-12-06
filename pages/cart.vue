<template>
  <div class="cart">
    <h2>Your Cart</h2>
    <hr>
    <div class="product" v-for="product in getCart" :key="product._id">
      <h2>{{product.title}}</h2>
      <h5>Quantity: {{product.quantity}}</h5>
      <h4>$ {{product.price * product.quantity}}</h4>
      <!-- <div>{{product.rating}}</div> -->
       <img :src="'http://localhost:5000/'+ product.photo"/>
        Qty:
       <select @change="onChangeQuantity($event, product)">
         <option v-for="i in 10" :key="i" :value="i" :selected="checkQty(product.quantity, i)">
           &nbsp;{{i}}
         </option>
       </select>
      <button class="btn btn-dark" @click="$store.commit('removeProduct', product)">Remove</button>
      <nuxt-link :to="'/products/'+product._id" class="btn btn-dark">Product Details</nuxt-link>
<!--
      <div>
          <h3>Description:</h3>
          <p>{{product.description}}</p>
      </div> -->
    </div>
    <hr>
    <h3>Subtotal({{getCartLength}} items): ${{getCartTotalPrice}}</h3>
    <button class="btn btn-dark">
      <nuxt-link to="/placeorder">Proceed to Checkout
    </nuxt-link></button>
    <nuxt-link to="/placeorder">
    </nuxt-link>
  </div>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
  computed: {
    ...mapGetters(["getCart", "getCartTotalPrice", "getCartLength"])
  },
  methods: {
    onChangeQuantity(event, product){
      let qty = parseInt(event.target.value)
      this.$store.commit("changeQty", { product, qty });
    },

    checkQty(prodQty, qty){
      if(parseInt(prodQty) === parseInt(qty)){
        return true;
      } else {
        return false;
      }
    }
  },
}
</script>

<style scoped>
.product{
  margin: 20px;
  padding: 20px;
  border: 1px solid lightgray;
}
.cart{
margin: 20px;
}
a{
  text-decoration: none;
  color: white;
}
img{
  height: 300px;
  width: 250px;
}
button{
  margin: 20px;
}
</style>
