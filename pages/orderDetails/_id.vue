<template>
  <div>
    <div class="order">
      <h5>OrderId:{{order._id}} </h5>
      <h4>Order Total: ${{orderTotal}}</h4>
      <div class="products">
        <div class="product" v-for="product in order.products" :key="product._id">
        <h4>{{product.prodId.title}}</h4>
        <img :src="'http://localhost:5000/'+ product.prodId.photo" alt="">
        <p>Price: {{product.price}}</p>
        <p>Quantity:{{product.quantity}}</p>
        <nuxt-link :to="'/reviews/'+ product.prodId._id" class="btn btn-dark">Add Review</nuxt-link>
        </div>
      </div>
    </div>

    <nuxt-link to="/orders" class="backbtn btn btn-dark">Back</nuxt-link>

  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }){
    try{
      let response = await $axios.$get(`http://localhost:5000/order/orderDetails/${params.id}`)
      let orderTotal = 0;
      response.order.products.map((item) => {
        orderTotal = orderTotal + (item.quantity * item.price);
      })
      return{
        order: response.order,
        orderTotal: orderTotal
      }
  }catch(err){
      console.log(err)
    }
  }
}
</script>

<style scoped>
.backbtn{
    margin: 0 auto;
    display: block;
    width: 100px;
}
.order{
  margin:20px
}
.products{
  border: 3px solid lightgray;
  padding: 10px;
}
</style>
