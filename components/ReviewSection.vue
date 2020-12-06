<template>
  <div>
    <h3>Product Review</h3>
    <div class="review-body" v-for="review in reviews" :key="review._id">
      <p>User: {{review.user}}</p>
      <h4>{{review.headline}}</h4>
      <p>{{review.body}}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product", "reviews"],
}
</script>

<style scoped>
.review-body{
  text-align: left;
  margin: 20px;
  padding: 10px;
  border: 1px solid lightgray;
  border-radius: 10px;
  box-shadow: 5px 5px lightgray;
}
.h3{
  text-align: left;
  margin-left: 20px;
}
</style>

