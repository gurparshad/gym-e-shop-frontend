<template>
<div>
  <div class="productDetails">
      <h3>{{product.title}}</h3>
      <h3>$ {{product.price}}</h3>
      <img class="prodImage" :src="'http://localhost:5000/'+ product.photo"/>
      <button class="btn btn-dark" @click="addProductToCart(product)">Add to Cart</button>
      <div class="productDesc">
          <h3>Description</h3>
          <p>{{product.description}}</p>
          <h3>Rating</h3>
          <p>⭐⭐⭐⭐⭐</p>
      </div>
              <div class="reviewSection">
          <ReviewSection :product="product" :reviews="reviews" />
      </div>
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
    width: 800px;
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-left: auto;
    margin-right: auto;
}

.prodImage{
  height: 350px;
  width: 300px;
  object-fit: contain;
  border-radius: 10px;
  margin: 10px;
}

.productDesc{
  margin: 20px;
}

.reviewSection{
  width: 800px;
  justify-content: center;
  margin-left: auto;
  margin-right: auto;
}
</style>
