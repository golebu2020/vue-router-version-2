<template>
  <h1>Login Page</h1>
  <div class="checking-container" v-if="productData.length > 0">
    <div v-for="data in productData" :key="data.id">
      <router-link
        class="product-container"
        :to="{ name: 'productDetail', params: { id: data.id } }"
      >
        <img class="product-image" :src="data.thumbnail" alt="" />
        <div class="product-info">
          <h3>{{ data.title }}</h3>
          <p>{{ data.brand }}</p>
        </div>
      </router-link>
    </div>
  </div>
  <div v-else>Loading Products...</div>
</template>
<script>
export default {
  data() {
    return {
      productData: [],
    };
  },

  mounted() {
    fetch("https://dummyjson.com/products")
      .then((res) => res.json())
      .then((data) => {
        this.productData = data.products;
      })
      .catch((err) => console.log(err.message));
  },
};
</script>
<style scoped>
.checking-container {
  margin: auto 30vw;
}
.product-image {
  width: 250px;
  border-radius: 8px;
  margin-right: 15px;
  object-fit: cover;
  transition: all 0.3s cubic-bezier(0.39, 0.575, 0.565, 1);
}
.product-image:hover {
  transform: scale(1.05, 1.05);
}
.product-container {
  display: flex;
  height: 200px;
  border-style: none;
  border-radius: 5px;
  padding: 10px;
  cursor: pointer;
  margin-bottom: 10px;
  box-shadow: 1px 1px 2px 1px rgba(0, 0, 0, 0.12);
  overflow: hidden;
}

.product-info {
  display: flex;
  flex-direction: column;
  align-items: start;
}
</style>
