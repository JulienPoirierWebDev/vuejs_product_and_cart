<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <ProductCard
        v-for="(product, index) in inventory"
        :key="product.id"
        :addToCart="addToCart"
        :index="index"
        :product="product"
      />
    </div>
  </main>
</template>

<script>
import ProductCard from '@/components/ProductCard'

export default {
  name: 'ProductsView',
  props: ['inventory', 'addToCart'],
  components: { ProductCard }
}
</script>

<style scoped>

</style>
