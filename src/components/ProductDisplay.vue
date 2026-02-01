<template>
  <div class="container" :class="containerClass">

    <div v-if="showModal" class="modal-overlay">
      <div class="modal-box">
        <h3>Haloo, Selamat Datang!</h3>
        <p>Project ini adalah katalog produk yang mengambil data langsung dari <b>FakeStoreAPI</b> (Index 1-20).</p>

        <div class="info-list">
          <div class="info-item">
            <span class="badge men">4</span>
            <span>Pakaian Pria</span>
          </div>
          <div class="info-item">
            <span class="badge women">6</span>
            <span>Pakaian Wanita</span>
          </div>
          <div class="info-item">
            <span class="badge unavailable">10</span>
            <span>Tidak Tersedia (Kategori Lain)</span>
          </div>
        </div>

        <p class="note">Klik tombol "Next Product" untuk melihat produk selanjutnya.</p>

        <button class="btn-start" @click="closeModal">Mulai Sekarang</button>
      </div>
    </div>

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
          <img src="../assets/sad-face.png" alt="Sad Face" class="sad-face-img">
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
      // Data Produk
      index: 1, // Index produk saat ini (mulai dari 1)
      product: {},

      // Status UI (Loading, Error, Modal)
      loading: false,
      isUnavailable: false, // True jika kategori bukan Pria/Wanita
      showModal: true, // Mengontrol visibilitas modal selamat datang
      categoryClass: '' // Helper untuk mengatur tema CSS dinamis
    }
  },
  computed: {
    /**
     * Menentukan class CSS untuk container utama berdasarkan kategori produk.
     * Output: 'page-men', 'page-women', atau 'page-unavailable'
     */
    containerClass () {
      return {
        'page-men': this.categoryClass === "men's clothing",
        'page-women': this.categoryClass === "women's clothing",
        'page-unavailable': this.isUnavailable
      }
    }
  },
  methods: {
    /**
     * Mengambil data produk dari FakeStoreAPI berdasarkan index saat ini.
     * Menangani status loading dan logika filter kategori.
     */
    async getProduct () {
      this.loading = true

      // Reset index ke 1 jika melebihi jumlah produk di API (20)
      if (this.index > 20) {
        this.index = 1
      }

      try {
        const response = await fetch(`https://fakestoreapi.com/products/${this.index}`)
        const data = await response.json()

        // Filter Bisnis: Hanya tampilkan kategori Pakaian Pria atau Wanita
        if (data.category === "men's clothing" || data.category === "women's clothing") {
          this.product = data
          this.isUnavailable = false
          this.categoryClass = data.category
        } else {
          // Fallback untuk kategori yang tidak didukung (Elektronik, Perhiasan, dll)
          this.isUnavailable = true
          this.categoryClass = 'unavailable'
        }
      } catch (error) {
        console.error('Gagal mengambil data:', error)
        this.loading = false
      } finally {
        this.loading = false
      }
    },

    nextProduct () {
      this.index++
      this.getProduct()
    },

    closeModal () {
      this.showModal = false
    }
  },
  mounted () {
    // Panggil API pertama kali saat komponen dimuat
    this.getProduct()
  }
}
</script>
