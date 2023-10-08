<template>
  <div>
    <section style="margin-left: -13%">
      <div class="container">
        <div class="row">
          <div class="col-lg-10 col-md-8 ml-auto">
            <div class="row align-items-center pt-md-5 mt-md-5 mb-5">
              <div class="col-12">
                <div class="card">
                  <div class="card-title text-center mt-3">
                    <h3>Add Product</h3>
                  </div>
                  <div class="card-body">
                    <form id="tambah-products" @submit.prevent="onFormSubmit">
                      <input
                        id="id"
                        v-model="productId"
                        name="id"
                        type="hidden"
                        class="form-control"
                      >
                      <div class="form-group">
                        <label for="title">Product Name:</label>
                        <input
                          id="title"
                          v-model="title"
                          name="title"
                          type="text"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product Name Can't Be Empty
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="brand">Product Brand:</label>
                        <input
                          id="brand"
                          v-model="brand"
                          name="brand"
                          type="text"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product ID Can't Be Empty
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="harga">Product Price:</label>
                        <input
                          id="harga"
                          v-model="harga"
                          name="harga"
                          type="number"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product Price Can't Be Empty
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="gambar">Product Image:</label>
                        <input
                          id="gambar"
                          v-model="gambar"
                          name="gambar"
                          type="text"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product Image Can't Be Empty and input url image
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="size">Product Size:</label>
                        <input
                          id="size"
                          name="size"
                          type="text"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product Size Can't Be Empty
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="deskripsi">Product Deskripsi:</label>
                        <input
                          id="deskripsi"
                          name="deskripsi"
                          type="text"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product Deskripsi Can't Be Empty
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="stok">Product Stock:</label>
                        <input
                          id="stok"
                          name="stok"
                          type="number"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product Stock Can't Be Empty
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="kategori">Product Category:</label>
                        <input
                          id="kategori"
                          name="kategori"
                          type="text"
                          class="form-control"
                        >
                        <div class="invalid-feedback">
                          Product Stok Can't Be Empty and input url image
                        </div>
                      </div>
                      <!-- <p>Product Image:</p>
                          <div class="custom-file">
                            <input
                              id="productimage"
                              type="file"
                              class="custom-file-input"
                              required
                            >
                            <label
                              class="custom-file-label"
                              for="productimage"
                            >Choose file...</label>
                            <div class="invalid-feedback">
                              File Format Not Supported
                            </div>
                          </div> -->
                      <button
                        class="btn btn-dark mt-5 mx-auto d-block"
                        type="submit"
                      >
                        Edit Products
                      </button>
                    </form>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
export default {
  layout (context) {
    return 'CustomDefault'
  },
  data () {
    return {
      title: ' ',
      brand: ' ',
      harga: 0,
      gambar: ' ',
      productId: ''
    }
  },
  mounted () {
    const params = this.$route.params
    // eslint-disable-next-line quotes
    this.getCartProduct(params?.id)
  },
  methods: {
    async getCartProduct (productId) {
      const response = await fetch(
        `https://jylpaciooxarhelwslji.supabase.co/rest/v1/products?id=eq.${productId}`,
        {
          headers: {
            apikey:
              'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imp5bHBhY2lvb3hhcmhlbHdzbGppIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTU3MjIxODYsImV4cCI6MjAxMTI5ODE4Nn0.DxbkTiy25jW5QSd3FgEvZm2G21JzU9kbcBSCdkOvmrU'
          }
        })
      const data = await response.json()
      // console.log(data)
      this.title = data[0]?.title
      this.brand = data[0]?.brand
      this.gambar = data[0]?.gambar
      this.harga = data[0]?.harga
      this.deskripsi = data[0]?.deskripsi
      this.size = data[0]?.size
      this.stok = data[0]?.stok
      this.kategori = data[0]?.kategori
      this.productId = data[0]?.id
    },
    async onFormSubmit () {
      //   const tambahProducts = document.getElementById('tambah-products')
      //   // eslint-disable-next-line no-use-before-define, new-cap
      //   const formData = new formData(tambahProducts)
      const dataForm = {
        title: document.getElementById('title').value,
        brand: document.getElementById('brand').value,
        harga: document.getElementById('harga').value,
        gambar: document.getElementById('gambar').value,
        id: document.getElementById('id').value,
        deskripsi: document.getElementById('deskripsi').value,
        kategori: document.getElementById('kategori').value,
        stok: document.getElementById('stok').value,
        size: document.getElementById('size').value
      }
      // console.log(dataForm)
      const response = await fetch(
        'https://jylpaciooxarhelwslji.supabase.co/rest/v1/products?id=eq.' + this.productId,
        {
          // eslint-disable-next-line quotes
          method: 'PATCH',
          headers: {
            apiKey:
              'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imp5bHBhY2lvb3hhcmhlbHdzbGppIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTU3MjIxODYsImV4cCI6MjAxMTI5ODE4Nn0.DxbkTiy25jW5QSd3FgEvZm2G21JzU9kbcBSCdkOvmrU',
            // eslint-disable-next-line quotes
            'Content-Type': 'application/json',
            // eslint-disable-next-line quotes
            Prefer: 'return=representation'
          },
          body: JSON.stringify(dataForm)
        }
      )
      console.log(response)
      const data = await response?.json()
      this.$router.push(`/app/cart/${data[0]?.id}`)
    }
  }
}
</script>
