<template>
  <div class="container" :class="containerClass">

    <div class="product-card">

      <div v-if="loading" class="loader-container">
        <div class="loader"></div>
      </div>

      <div v-else style="width: 100%">

        <div v-if="!isUnavailable" class="product-content">
          <div class="product-image">
            <img :src="product.image" :alt="product.title">
          </div>

          <div class="product-details">
            <h2 class="title">{{ product.title }}</h2>

            <div class="category-row">
                <span>{{ product.category }}</span>

                <div class="rating-container">
                    <span style="margin-right: 10px; font-weight: 700;">{{ product.rating && product.rating.rate }}/5</span>
                    <div
                        v-for="i in 5"
                        :key="i"
                        class="circle"
                        :class="{ 'filled': i <= (product.rating ? Math.round(product.rating.rate) : 0) }"
                    ></div>
                </div>
            </div>

            <div class="description">
              <p>{{ product.description }}</p>
            </div>

            <div class="price">${{ product.price }}</div>

            <div class="actions">
              <button class="btn btn-buy">Buy now</button>
              <button class="btn btn-next" @click="nextProduct">Next product</button>
            </div>
          </div>
        </div>

        <div v-else class="unavailable-content">
            <div class="sad-face">
                <div class="eyes-container">
                <div class="eye left"></div>
                <div class="eye right"></div>
                </div>
                <div class="mouth"></div>
            </div>
            <p class="unavailable-text">This product is unavailable to show</p>
            <button class="btn btn-next" @click="nextProduct">Next product</button>
        </div>

      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductDisplay',
  data () {
    return {
      index: 1, // Mulai dari index 1
      product: {}, // Data produk
      loading: false, // Status loading
      isUnavailable: false, // Status availability
      categoryClass: '' // Helper untuk class CSS
    }
  },
  computed: {
    // Menentukan class CSS berdasarkan kategori
    containerClass () {
      return {
        'page-men': this.categoryClass === "men's clothing",
        'page-women': this.categoryClass === "women's clothing",
        'page-unavailable': this.isUnavailable
      }
    }
  },
  methods: {
    async getProduct () {
      this.loading = true // Nyalakan spinner

      // Reset index jika melebihi 20 (Sesuai Hint Dokumen)
      if (this.index > 20) {
        this.index = 1
      }

      try {
        const response = await fetch(`https://fakestoreapi.com/products/${this.index}`)
        const data = await response.json()

        // Cek apakah kategori sesuai yang diminta
        if (data.category === "men's clothing" || data.category === "women's clothing") {
          this.product = data
          this.isUnavailable = false
          this.categoryClass = data.category // Set class warna
        } else {
          // Jika kategori BUKAN Men/Women, masuk ke mode Unavailable
          this.isUnavailable = true
          this.categoryClass = 'unavailable' // Set class abu-abu
        }
      } catch (error) {
        console.error('Error fetching data:', error)
        this.loading = false
      } finally {
        this.loading = false // Matikan spinner
      }
    },
    nextProduct () {
      this.index++ // Increment index
      this.getProduct() // Panggil API lagi
    }
  },
  mounted () {
    this.getProduct() // Panggil API pertama kali saat web dibuka
  }
}
</script>
