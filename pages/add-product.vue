<template>
  <div>
    <TheProductsHeader />
    <section id="sectionProduct" class="sectionPad">
      <div class="containerGrid">
        <div
          v-for="(product, index) in products"
          :key="index"
          class="proGrid"
          :product="product"
        >
          <img :src="product.gambar" alt="gambar-products">
          <div class="productDeskripsi">
            <span>{{ product.brand }}</span>
            <span>{{ product.detail ? 'sudah dibeli' : 'belum dibeli' }}</span>
            <h5>{{ product.title }}</h5>
            <div class="star">
              <i class="fas fa-star" />
              <i class="fas fa-star" />
              <i class="fas fa-star" />
              <i class="fas fa-star" />
              <i class="fas fa-star" />
            </div>
            <h4>Rp.{{ product.harga }}.000</h4>
          </div>
          <nuxt-link
            class="BuyRoleButton"
            :to="'app/detail/' + product.id"
          >
            Beli
          </nuxt-link>
          <a href="#"><i class="fal fa-shopping-cart cart" /></a>
        </div>
      </div>
    </section>
    <form
      class="add-card"
      style="
        display: inline-flex;
        flex-wrap: wrap;
        align-items: baseline;
        flex-direction: column;
        width: 40rem;
        margin: 10px 7%;
      "
      @submit.prevent="onSubmit"
    >
      <div class="card mb-2">
        <div class="card-body d-flex flex-column p-0">
          <input
            v-model="product.title"
            class="form-control border-0 mb-2"
            placeholder="Title"
            type="text"
          >
          <textarea
            v-model="product.description"
            class="form-control border-0 small"
            placeholder="Description"
            rows="3"
          />
          <input
            v-model="product.brand"
            class="form-control border-0 mb-2"
            placeholder="Title"
            type="text"
          >
          <input
            v-model="product.harga"
            class="form-control border-0 mb-2"
            placeholder="Title"
            type="text"
          >
          <input
            v-model="product.gambar"
            class="form-control border-0 mb-2"
            placeholder="Title"
            type="text"
          >
          <input
            v-model="product.detail"
            class="form-control border-0 mb-2"
            placeholder="Title"
            type="text"
          >
        </div>
      </div>
      <div class="button-wrapper d-flex">
        <button class="btn btn-primary me-2" type="submit">
          Save
        </button>
        <button
          class="btn btn-outline-secondary"
          @click="isCreating = !isCreating"
        >
          Cancel
        </button>
      </div>
    </form>
  </div>
</template>
<script>
import { mapActions } from 'vuex'
import TheProductsHeader from '~/components/products/TheProductsHeader.vue'

export default {
  components: {
    TheProductsHeader
  },
  layout (context) {
    return 'CustomDefault'
  },
  data () {
    return {
      product: [
        {
          id: 4,
          title: '',
          description: '',
          brand: '',
          gambar: '',
          harga: 0,
          detail: false
        }
      ]
    }
  },
  computed: {
    products () {
      return this.$store.state.products.products
    }
  },
  methods: {
    ...mapActions('products', ['addProducts']),
    onSubmit () {
      // memperbaharui task id
      this.product.id += 1
      // agar tidak terjadi konflik saat perubahan data
      const payload = this.product
      // proses pemanggilan action ('nama_file/nama_method', parameter)
      // this.$store.commit('ADD_TASK', payload)
      this.addProducts(payload)
      // mengembalikan isi form seperti semula
      this.product = {
        title: '',
        description: '',
        brand: '',
        gambar: '',
        harga: 0,
        rating: null,
        detailProducts: null,
        detail: false
      }
    }
  }
}
</script>

<style scoped>
h1 {
  font-size: 50px;
  line-height: 64px;
  color: #222;
}

h2 {
  font-size: 46px;
  line-height: 54px;
  color: #222;
}

h4 {
  font-size: 20px;
  color: #222;
}

h6 {
  font-weight: 700;
  font-size: 12px;
}

p {
  font-size: 16px;
  color: #465b52;
  margin: 15px 0 20px 0;
}

body {
  width: 100%;
}

#sectionProduct {
  text-align: center;
}

.sectionPad {
  padding: 0 80px;
}

#sectionProduct .containerGrid {
  display: contents;
  justify-content: space-between;
  padding-top: 20px;
  align-items: center;
  flex-wrap: wrap;
}

#sectionProduct .proGrid {
  width: 23%;
  min-width: 250px;
  padding: 10px 12px;
  border: 1px solid #cce7d0;
  border-radius: 25px;
  cursor: pointer;
  box-shadow: 20px 20px 30px rgba(0, 0, 0, 0.02);
  margin: 15px 10px;
  transition: 0.2s ease;
  position: relative;
  float: left;
}

#sectionProduct .proGrid:hover {
  box-shadow: 20px 20px 30px rgba(0, 0, 0, 0.06);
}

#sectionProduct .proGrid img {
  width: 100%;
  border-radius: 20px;
}

#sectionProduct .proGrid .productDeskripsi {
  text-align: start;
  padding: 10px 0;
}

#sectionProduct .proGrid .productDeskripsi span {
  color: #606063;
  font-size: 12px;
}

#sectionProduct .proGrid .productDeskripsi h5 {
  padding-top: 7px;
  color: #1a1a1a;
  font-size: 14px;
  font-weight: 700;
}

#sectionProduct .proGrid .productDeskripsi i {
  font-size: 12px;
  color: rgb(243, 181, 25);
}

#sectionProduct .proGrid .productDeskripsi h4 {
  padding-top: 7px;
  font-size: 15px;
  font-weight: 700;
  color: #088178;
}

#sectionProduct .proGrid .cart {
  width: 40px;
  height: 40px;
  line-height: 40px;
  border-radius: 50px;
  background-color: #e8f6ea;
  font-weight: 500;
  color: #088178;
  border: 1px solid #cce7d0;
  position: absolute;
  bottom: 20px;
  right: 10px;
}

.BuyRoleButton {
  text-decoration: none;
  position: absolute;
  bottom: 23px;
  right: 60px;
  color: #fff;
  border-radius: 5px;
  /* border: 1px solid #080808; */
  background-color: #088178;
  padding: 4px 11px;
  font-size: 15px;
  font-weight: 500;
}

.BuyRoleButton:hover {
  background-color: #078d84c0;
  opacity: 0.9;
}
</style>
