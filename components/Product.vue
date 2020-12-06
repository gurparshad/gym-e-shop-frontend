 <template>
  <div >
       <NuxtLink :to="'/products/' + productId">
          <img :src="'http://localhost:5000/'+ productPhoto" alt="product-image"/>
          <h2>{{productTitle}}</h2>
        </NuxtLink>


      <!-- <div>{{productRating}}</div> -->
      <h3>${{productPrice}}</h3>
       <p>⭐⭐⭐⭐⭐</p>
       <nuxt-link :to="'/products/' + productId">
       <template v-if="productDetailsButton">
         <button class="btn btn-dark">Details</button>
       </template>

       </nuxt-link>


  </div>
</template>
<script>
export default {

    name: 'Product',
    props: ['productId','productPrice', 'productTitle', 'productRating', 'productPhoto', 'productDetailsButton'],
}
</script>

<style scoped>
a, a:hover, a:focus, a:active{
  text-decoration: none;
  color: inherit;
}
img{
  border-radius: 20px;
  height: 300px;
  width: 250px;
  transition: transform 250ms;
}
img:hover{
  transform: scale(1.03);
}
</style>
