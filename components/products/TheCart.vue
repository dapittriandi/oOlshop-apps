<template>
  <section class="h-100" style="background-color: #eee">
    <div class="container h-100 py-5">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-10">
          <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 class="fw-normal mb-0 text-black">
              Shopping Cart
            </h3>
            <div>
              <p class="mb-0">
                <span class="text-muted">Sort by:</span>
                <a
                  href="#!"
                  class="text-body"
                >Price <i class="fas fa-angle-down mt-1" /></a>
              </p>
            </div>
          </div>

          <div class="card rounded-3 mb-4">
            <div class="card-body p-4">
              <div
                class="row d-flex justify-content-between align-items-center"
              >
                <div class="col-md-2 col-lg-2 col-xl-2">
                  <img
                    :src="gambar"
                    class="img-fluid rounded-3"
                    alt="Cotton T-shirt"
                  >
                </div>
                <div class="col-md-3 col-lg-3 col-xl-3">
                  <p class="lead fw-normal mb-2">
                    {{ title }}
                  </p>
                  <p>
                    <span class="text-muted">Size: </span> M
                    <span class="text-muted">brand: </span>{{ brand }}
                  </p>
                </div>
                <div class="col-md-3 col-lg-3 col-xl-2 d-flex">
                  <button
                    class="btn btn-link px-2"
                    onclick="this.parentNode.querySelector('input[type=number]').stepDown()"
                  >
                    <i class="fas fa-minus" />
                  </button>

                  <input
                    id="form1"
                    min="0"
                    name="quantity"
                    value="2"
                    type="number"
                    class="form-control form-control-sm"
                  >

                  <button
                    class="btn btn-link px-2"
                    onclick="this.parentNode.querySelector('input[type=number]').stepUp()"
                  >
                    <i class="fas fa-plus" />
                  </button>
                </div>
                <div class="col-md-3 col-lg-2 col-xl-2 offset-lg-1">
                  <h5 class="mb-0">
                    Rp.{{ harga }}.000
                  </h5>
                </div>
                <div class="col-md-1 col-lg-1 col-xl-1 text-end">
                  <a
                    href="#!"
                    class="text-danger"
                  ><i class="fas fa-trash fa-lg" /></a>
                </div>
              </div>
            </div>
          </div>
          <div class="card mb-4">
            <div class="card-body p-4 d-flex flex-row">
              <div class="form-outline flex-fill">
                <input
                  id="form1"
                  type="text"
                  class="form-control form-control-lg"
                >
                <label class="form-label" for="form1">Discound code</label>
              </div>
              <button type="button" class="btn btn-outline-warning btn-lg ms-3">
                Apply
              </button>
            </div>
          </div>

          <div class="card">
            <div class="card-body">
              <button type="button" class="btn btn-warning btn-block btn-lg">
                Proceed to Pay
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  layout (context) {
    return 'CustomDefault'
  },
  props: {
    // product: {
    //   type: Object,
    //   required: true,
    //   default: () => {}
    // }
  },
  data () {
    return {
      title: ' ',
      brand: ' ',
      harga: 0,
      gambar: ' '
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
        }
      )
      const data = await response.json()
      this.title = data[0].title
      this.brand = data[0].brand
      this.gambar = data[0].gambar
      this.harga = data[0].harga
    }
  }
}
</script>
