<template>
  <div>
    <div class="container mb-5">
      <img :src="product.image" :alt="product.title" class="img-fluid productImg">
      <h2 class="product-title">{{ product.title }}</h2>
      <p class="product-price">{{ product.price }}</p>
      <p class="product-category">{{ product.category }}</p>
      <p class="product-description">{{ product.description }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const product = ref({})

const fetchProduct = async () => {
  const response = await fetch(`https://fakestoreapi.com/products/${route.params.id}`)
  const data = await response.json()
  product.value = data
}

onMounted(fetchProduct)
</script>

<style scoped>

.container{
  max-width: 1200px;
}
.product-card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

.productImg {
  height: 400px;
}

.product-title {
  font-size: 24px;
  font-weight: bold;
  margin: 10px 0;
}

.product-price {
  color: #007BFF;
  font-size: 20px;
  margin: 10px 0;
}

.product-category {
  font-size: 18px;
  color: #6c757d;
  margin: 10px 0;
}

.product-description {
  font-size: 16px;
  margin: 10px 0;
}
</style>
