<template>
  <div>
    <div>
      <TheNavbarProduct />
    </div>
    <TheProductsHeader />
    <section id="sectionProduct" class="sectionPad">
      <div class="containerGrid">
        <div
          v-for="(product, index) in products"
          :key="index"
          class="proGrid"
          :product="product"
          :title="product?.title"
          :brand="product?.brand"
          :gambar="product?.gambar"
          :harga="product?.harga"
          :detail="product?.detail"
        >
          <img :src="product.gambar" alt="gambar-products">
          <div class="productDeskripsi">
            <span>{{ product.brand }}</span>
            <!-- <span>{{ product.detail ? 'sudah dibeli' : 'belum dibeli' }}</span> -->
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
          <!-- <nuxt-link class="BuyRoleButton" :to="'detail/' + product.id">
            Beli
          </nuxt-link> -->
          <nuxt-link :to="'cart/' + product.id">
            <i class="fal fa-shopping-cart cart" />
          </nuxt-link>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import TheNavbarProduct from '~/components/products/TheNavbarProduct.vue'
// import httpClient from '~/utils/httpClient.js'
// import axios from '~/plugin/axios.js'
import TheProducts from '~/components/products/TheProducts.vue'
import TheProductsHeader from '~/components/products/TheProductsHeader.vue'
export default {
  name: 'ProductPage',
  // eslint-disable-next-line vue/no-unused-components
  components: {
    // eslint-disable-next-line vue/no-unused-components
    TheProducts,
    TheProductsHeader,
    TheNavbarProduct
  },
  layout (context) {
    return 'CustomDefault'
  },
  data () {
    return {
      products: []
    }
  },
  mounted () {
    this.getProducts()
    console.log(this.products)
  },
  methods: {
    async getProducts () {
      await this.$axios
        .$get('https://jylpaciooxarhelwslji.supabase.co/rest/v1/products', {
          headers: {
            apikey:
              'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imp5bHBhY2lvb3hhcmhlbHdzbGppIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTU3MjIxODYsImV4cCI6MjAxMTI5ODE4Nn0.DxbkTiy25jW5QSd3FgEvZm2G21JzU9kbcBSCdkOvmrU'
          }
        })
        .then((res) => {
          res.map(data => this.products.push(data))
        })
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
</style>
