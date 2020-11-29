 <template>
  <div>
       <NuxtLink :to="'/products/' + productId">
          <img src="/impact-whey-protein.jpg" alt="product-image"/>
        </NuxtLink>

      <h2>{{productTitle}}</h2>
      <!-- <div>{{productRating}}</div> -->
      <h3>${{productPrice}}</h3>
      <button>
        <nuxt-link to="/cart">
           Add to Cart </nuxt-link></button>
      <button>Buy Now</button>
  </div>
</template>
<script>

export default {
    name: 'Product',
    props: ['productId','productPrice', 'productTitle', 'productRating']
}
</script>

<style scoped>
a, a:hover, a:focus, a:active{
  text-decoration: none;
  color: inherit;
}
</style>
