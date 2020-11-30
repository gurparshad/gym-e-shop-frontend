<template>
<div class="order-page">
  <h2>Your Orders</h2>
  {{$auth.state.user.name}}
  <div v-for="order in orders" :key="order._id">
    <h3>Order ID:{{order._id}}</h3>
    <div class="orders-products">
      <div class="product" v-for="product in order.products" :key="product._id">
         <!-- <img :src="'http://localhost:5000/'+ product.photo"/> -->
        <p>Product ID:{{product._id}}</p>
        <p>Quantity:{{product.quantity}}</p>
        <p>Price: {{product.price}}</p>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try{
      console.log("here my friend");
      let response = await $axios.$get('http://localhost:5000/order/allOrders');
      console.log("hey man",response);

      return {
        orders: response.products
      }
    }catch(err){
      console.log(err)
    }
  },
}
</script>

<style scoped>
.order-page{
  margin: 20px;
}

.orders-products{
  border: 1px solid lightgray;
  padding: 20px;
}

</style>
