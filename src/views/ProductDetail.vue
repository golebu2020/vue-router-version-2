<template>
  <div v-if="data !== null" class="detail-container">
    <h2>{{ data.title }}</h2>
    <h3>{{ data.description }}</h3>
    <h2>{{ data.category }}</h2>
    <p>${{ data.price }}</p>
  </div>
  <div v-else>Please wait...</div>
</template>
<script>
export default {
  props: ["id"],
  data() {
    return {
      data: {},
    };
  },
  mounted() {
    fetch("https://dummyjson.com/products/" + this.id)
      .then((res) => res.json())
      .then((data) => {
        this.data = data;
      })
      .catch((err) => console.log(err.message));
  },
};
</script>
<style>
.detail-container {
  margin: auto 500px;
  text-align: start;
}
</style>
