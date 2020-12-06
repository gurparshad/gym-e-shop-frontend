<template>
<div class="order-page">
  <h2>Your Orders</h2>
  <div v-for="order in orders" :key="order._id">

    <h4>
      Order Id: {{order._id}}
      </h4>
    <div class="orders-products">
      <div class="product" v-for="product in order.products" :key="product._id">
        <h4>{{product.prodId.title}}</h4>
        <img :src="'http://localhost:5000/'+ product.prodId.photo" alt="">
        </div>
        <nuxt-link :to="'/orderDetails/' + order._id" class="btn btn-dark">Order Details</nuxt-link>

    </div>
  </div>
</div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try{
      let response = await $axios.$get('http://localhost:5000/order/allOrders');

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

a{
  text-decoration: none;
  color: rgb(87, 188, 231);
}
.order-page{
  margin: 20px;
}

.orders-products{
  border: 1px solid lightgray;
  padding: 20px;
}

.btn{
  margin: 20px;
  color: white;
}

img{
  width: 300px;
  height: 300px;
}

.product{
  margin: 20px;
}

</style>
