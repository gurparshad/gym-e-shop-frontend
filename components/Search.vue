<template>
  <div >
    <div class="searchSection">
    <label for="search">Find a Product</label>
    <input type="text" v-model="query" autocomplete="off" @input="filterProducts" @focus="modal=true">
    <button @click="onSearch"  class="btn btn-dark">Search</button>
    </div>
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
.searchSection{
  display: flex;
  align-items: center;
}
.btn{
  margin: 10px;
}
label{
  margin: 10px;
}
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
