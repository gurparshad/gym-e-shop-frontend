<template>
  <div>
    <div class="address">
      <h3>Delivey Address</h3>
      <p>Name: {{addresses[0].fullName}}</p>
      <p>Street Address: {{addresses[0].streetAddress}}</p>
      <p>City: {{addresses[0].city}}</p>
      <p>Country: {{addresses[0].country}}</p>
      <p>Phone: {{addresses[0].phoneNumber}}</p>
    </div>
    <div class="products">
      <h3>Products in your Cart</h3>
      <div class="product" v-for="product in getCart" :key="product._id">
        <h4>{{product.title}}</h4>
         <img :src="'http://localhost:5000/'+ product.photo"/>
        <p>Price: {{(product.price * product.quantity).toFixed(2)}}</p>
        <p>Quantity: {{product.quantity}}</p>
      </div>
      <hr>
      <h3>Total Price:{{getCartTotalPrice}}</h3>
      <br>
      <nuxt-link to="/payment" class="btn btn-dark">Continue to payment page</nuxt-link>
    </div>

  </div>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
  computed: {
    ...mapGetters(["getCart", "getCartTotalPrice"])
  },
  async asyncData({ $axios}){
    try{
      let response = await $axios.$get('http://localhost:5000/address/getAddresses');

      return {
        addresses: response.addresses
      }
    }catch(err){
      console.log(err);
    }
  }
}

</script>

<style scoped>
.address{
  margin: 20px;
  border: 1px solid lightgray;
  padding: 10px;
  border-radius: 10px;
}
.products{
    margin: 20px;
  border: 1px solid lightgray;
  padding: 10px;
  border-radius: 10px;
}
img{
  width: 300px;
  height: 300px;
}
</style>
