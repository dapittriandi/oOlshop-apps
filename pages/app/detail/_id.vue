<template>
  <div class="container">
    <h1 style="text-align: center">
      Detail
    </h1>
    <div>
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
                    <span class="text-muted">View:</span>
                    <a
                      href="/app/product"
                      class="text-body"
                    >All Item <i class="fas fa-angle-down mt-1" /></a>
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
                        <span class="text-muted">Size: </span> {{ size }} <br>
                        <span class="text-muted">Brand: </span>{{ brand }}
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
                      <button style="border: none; outline: none; background: none" @click="deleteDataProducts(productId)">
                        <a
                          class="text-danger"
                          href="/app/product"
                        ><i class="fas fa-trash fa-lg" /></a>
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <!-- <div class="card mb-4">
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
          </div> -->

              <div class="card">
                <div class="card-body">
                  <button type="button" class="btn btn-danger btn-block btn-lg" @click="onEdit">
                    Edit
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
    <main>
      <div class="py-4">
        <div class="container">
          <div class="item-task d-flex align-items-start pt-3 pb-4">
            <div>
              <input
                id="task"
                type="checkbox"
                name="status"
                class="me-2 mt-2"
                :checked="product.detail"
                @change="changeStatus"
              >
              <div>
                <div class="title-task mb-1">
                  {{ product.brand }}
                </div>
                <div class="description-task small text-muted mb-3">
                  {{ product.title }}
                </div>
                <input class="form-control form-control-sm" type="date">
              </div>
              <div class="action mt-4">
                <div
                  class="btn btn-outline-secondary btn-sm mb-3"
                  @click="$router.go(-1)"
                >
                  Kembali
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
<script>
import { mapGetters, mapActions, mapState } from 'vuex'

export default {
  layout (context) {
    return 'CustomDefault'
  },
  data () {
    return {
      paramId: this.$route.params.id
    }
  },

  computed: {
    ...mapState('products', ['products']),
    ...mapGetters({
      getProductById: 'products/getProductById'
    }),
    product () {
      return this.getProductById(this.paramId)
    }
  },
  methods: {
    ...mapActions('products', ['updateStatus', 'addProducts']),
    changeStatus () {
      // eslint-disable-next-line no-undef
      this.updateStatus(this.product)
    }
  }
}
</script>
