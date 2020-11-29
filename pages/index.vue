<template>
  <div class="home">
    <div>
        <img class="bannerImage" src="/banner.png"/>
    </div>
    <div>
        <h1 class="head">All the product you need for a healthy lifestyle</h1>
        <div class="products">
          <div class="product" v-for="item in products" :key="item._id">
            <Product :product-id="item._id" :product-title="item.title"
            :product-price="item.price" :product-rating="item.rating"
          />
        </div>
    </div>
    <div class="bottom-banner">
      <div class="bottom-banner-child">
        <img src="/image1.jpg" alt="image">
        <h3>Push your limits Everyday</h3>
      </div>
      <div class="bottom-banner-child">
        <img src="/image2.jpg" alt="image">
        <h3>Cloths, Accessories, Equipments</h3>
        <button>Buy Now</button>
      </div>

    </div>
  </div>
  </div>
</template>

<script>
import Product from '../components/Product';
export default {
  name: 'Home',
  components: {
    Product,
  },

  async asyncData({$axios}){
    try{
      let response = await $axios.$get("http://localhost:5000/product/getAllProducts");
      console.log(response);
      return {
        products: response.products
      }
    }catch(err){
      console.log(err);
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.home{
  margin-bottom: 100px;
}

.bannerImage{
  object-fit: contain;
  width: 100%;
}

.head {
  text-align: center;
  margin-top: 20px;
}

.products{
  display: flex;
  justify-content: space-around;
  margin: 30px;
}

.bottom-banner{
  display: flex;
  justify-content: space-around;
  margin-top: 80px;
}

.bottom-banner-child{
  display: flex;
  flex-direction: column;
  margin-bottom: 50px;
}

</style>
