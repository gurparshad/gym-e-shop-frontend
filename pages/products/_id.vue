<template>
<div>
  <h3>Product Details</h3>
  <div class="productDetails">
      <h1>{{product.title}}</h1>
      <h3>$ {{product.price}}</h3>
      <!-- <div>{{product.rating}}</div> -->
      <img src="/impact-whey-protein.jpg"/>
      <button @click="addProductToCart(product)">Add to Cart</button>
      <div>
          <h3>Description:</h3>
          <p>{{product.description}}</p>
      </div>
      </div>
      <div class="reviewSection">
        <ReviewSection :product="product" :reviews="reviews" />
      </div>


  </div>
</template>

<script>
 import ReviewSection from "~/components/ReviewSection";
 import { mapActions } from 'vuex';
export default {
 components: {
   ReviewSection
 },

  async asyncData({ $axios, params}) {
    try {
      let singleProduct = await $axios.$get(`http://localhost:5000/product/getProduct/${params.id}`);
      let reviews = await $axios.$get(`http://localhost:5000/review/allReviews/${params.id}`)

      return {
        product: singleProduct.product,
        reviews: reviews.reviews
      }
    }catch(err){
      console.log(err);
    }
  },

  methods: {
    ...mapActions(["addProductToCart"])
  },
}
</script>

<style>
.productDetails{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
img{
  object-fit: contain;
}
.reviewSection{
  margin: 20px;
}
</style>
