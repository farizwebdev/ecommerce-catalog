<template>
  <div id="app">
    <ProductDisplay />
  </div>
</template>

<script>
import ProductDisplay from './components/ProductDisplay.vue'
import './assets/style/page.css' // Import CSS global di App.vue

export default {
  name: 'App',
  components: {
    ProductDisplay
  }
}
</script>
