<template>
  <div class="container">
    <div class="row gy-4">
      <div v-for="product in products" :key="product.id" class="col-12 col-md-4">
        <div class="card  h-100">
          <img :src="product.image" :alt="product.title" class="card-img-top">
          <div class="card-body">
            <h5 class="card-title">{{ product.title }}</h5>
            <p class="card-text">{{ product.description }}</p>
            <p class="card-text"><small class="text-muted">{{ product.category }}</small></p>
            <h5>${{ product.price }}</h5>
          </div>
          <div class="card-footer">
            <button @click="viewDetails(product.id)" class="btn btn-primary">View Details</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const products = ref([])

const fetchProducts = async () => {
  const response = await fetch('https://fakestoreapi.com/products')
  const data = await response.json()
  products.value = data
}

onMounted(fetchProducts)

const viewDetails = (id) => {
  router.push({ name: 'ProductDetails', params: { id } })
}
</script>


<style scoped>
.container{
  max-width: 1200px;
}
.product-card {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 20px;
  margin: 20px;
  max-width: 300px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s ease-in-out;
}

.product-card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.product-image {
  width: 100%;
  height: 200px;
}

.product-title {
  font-size: 18px;
  font-weight: bold;
  margin: 10px 0;
}

.product-price {
  color: #007BFF;
  font-size: 16px;
  margin: 10px 0;
}

.product-category {
  font-size: 14px;
  color: #6c757d;
  margin: 10px 0;
}

.product-description {
  font-size: 14px;
  margin: 10px 0;
}

.details-button {
  background-color: #007BFF;
  color: white;
  border: none;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 10px 2px;
  cursor: pointer;
  border-radius: 4px;
  transition-duration: 0.4s;
}

.details-button:hover {
  background-color: white;
  color: black;
  border: 2px solid #007BFF;
}
</style>
