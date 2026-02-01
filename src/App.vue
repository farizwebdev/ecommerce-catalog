<template>
  <div id="app">
    <ProductDisplay />
  </div>
</template>

<script>

// Components
import ProductDisplay from './components/ProductDisplay.vue'

// Global Styles
import './assets/style/page.css'

export default {
  name: 'App',
  components: {
    ProductDisplay
  }
}

</script>
