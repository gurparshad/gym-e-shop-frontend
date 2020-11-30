<template>
  <div>
    <label for="search">SearchProduct</label>
    <input type="text" v-model="query">
    <button @click="onSearch">Search</button>
  </div>
</template>

<script>
export default {
  name: 'Search',

data(){
    return {
      query: ""
    }
  },

  methods: {
    onSearch(){
      this.$router.push({
        path: "/search",
        query:{ title: this.query}
      })
    }
  }
}
</script>
