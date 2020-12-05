<template>
  <div>
    <div @click="modal=false"></div>
    <label for="search">SearchProduct</label>
    <input type="text" v-model="query" autocomplete="off" @input="filterProducts" @focus="modal=true">
    <button @click="onSearch">Search</button>
    <div class="searchSuggestions" v-if="filteredProducts && modal">
      <ul>
        <li v-for="filteredProduct in filteredProducts" :key="filteredProduct" @click="setSearchProduct(filteredProduct)">{{ filteredProduct}}</li>
      </ul>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Search',

data(){
    return {
      query: "",
      modal: false,
      products: [
        'Bag','Protein clear vegan','Whey Protein','Peanut butter'
      ],
      filteredProducts: [],
    }
  },

  methods: {
    onSearch(){
      this.$router.push({
        path: "/search",
        query:{ title: this.query}
      });
    },

    filterProducts(){
      this.filteredProducts = this.products.filter(query => {
        return query.toLowerCase().startsWith(this.query.toLowerCase());
      });
    },

    setSearchProduct(product){
      this.query = product;
      this.modal = false;
    }
  }
}
</script>

<style scoped>
ul{
  width: 300px;
  border: 1px lightgray solid;
}

li{
  list-style-type: none;
  padding: 5px 0;
  cursor:pointer;
}
</style>
