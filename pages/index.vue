<template>
  <div class="home">
    <div class="search">
      <Search/>
    </div>
    <div class="categories">
      <Categories :categories="categories"/>
    </div>
    <div class="main">

        <img class="bannerImage" src="/banner.png"/>
    </div>

    <div>
        <h1 class="head">Best Sellers</h1>
        <hr>
        <div class="products">
          <div class="product" v-for="item in products.slice(0, 4)" :key="item._id">
            <Product :product-id="item._id" :product-title="item.title"
            :product-price="item.price" :product-rating="item.rating"
            :product-photo="item.photo" :productDetailsButton="false"
          />
        </div>
    </div>
    <hr>

  </div>
  <h1 class="head">Everything you need for healthy lifestyle</h1>

      <div class="bottom-banner">
    <div class="card" style="width: 18rem;">
  <img class="card-img-top" src="/nutrition.jpg" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">Nutrition</h5>
    <p class="card-text">Nutrition is most important thing to live a healthy lifestyle. Whey protein, protein bars and many more</p>
     <NuxtLink class="btn btn-dark" to="/category/5fccad98fe30c5359835a92a">Shop Now</NuxtLink>
  </div>
</div>

      <div class="card" style="width: 18rem;">
  <img class="card-img-top" src="/equipment.jpg" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">Equipment</h5>
    <p class="card-text">Do you like to workout at home check our workout equipment collection, available at the best price</p>
     <NuxtLink class="btn btn-dark" to="/category/5fccadacfe30c5359835a92c">Shop Now</NuxtLink>
  </div>
</div>

      <div class="card" style="width: 18rem;">
  <img class="card-img-top" src="/clothes.jpg" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">Clothes</h5>
    <p class="card-text">Looking for perfect gym attire, check our brand new collection of amazing outfits for men and women</p>
    <NuxtLink class="btn btn-dark" to="/category/5fccada2fe30c5359835a92b">Shop Now</NuxtLink>
  </div>
</div>

      <div class="card" style="width: 18rem;">
  <img class="card-img-top" src="/accessories.jpg" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">Accessories</h5>
    <p class="card-text">Gym accessories are available now. Fancy bags, bands, shakers, and many more. Check now</p>
     <NuxtLink class="btn btn-dark" to="/category/5fccadbbfe30c5359835a92d">Shop Now</NuxtLink>
  </div>
</div>

  </div>
  </div>
</template>

<script>
import Product from '../components/Product';
import Search from '../components/Search';
import Categories from '../components/Categories';
export default {
  name: 'Home',
  components: {
    Product,
    Search,
    Categories
  },

  async asyncData({$axios}){
    try{
      let response = await $axios.$get("http://localhost:5000/product/getAllProducts");
      let response2 = await $axios.$get("http://localhost:5000/category/getCategories");
      return {
        products: response.products,
        categories: response2.categories,
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

.search{
  display: flex;
  justify-content: center;
  padding: 10px;
}

.bannerImage{
  object-fit: contain;
  width: 100%;
}

.head {
  text-align: center;
  margin-top: 30px;
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
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  margin-bottom: 50px;
}

.card{
  transition: transform 450ms;
}
.card:hover {
  transform: scale(1.06);
  box-shadow: 0 0 10px #515151;
  cursor: pointer;
}

.card-img-top{
  object-fit: contain;
  height: 300px;
}

</style>
