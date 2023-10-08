<template>
  <section class="vh-100" style="background-color: #eee">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col col-md-9 col-lg-7 col-xl-5">
          <div
            class="card"
            style="border-radius: 15px; background-color: #93e2bb"
          >
            <div
              v-for="(user, index) in pengguna"
              :key="index"
              class="card-body p-4 text-black"
              :user="user"
              :username="user?.username"
              :email="user?.email"
              :alamat="user?.alamat"
              :no_hp="user?.no_hp"
            >
              <div>
                <h6 class="mb-4">
                  {{ user.username }}
                </h6>
                <h6 class="mb-4">
                  {{ user.alamat }}
                </h6>
                <h6 class="mb-4">
                  {{ user.no_hp }}
                </h6>
                <div
                  class="d-flex align-items-center justify-content-between mb-3"
                >
                  <p class="small mb-0">
                    <i class="far fa-clock me-2" />3 hrs
                  </p>
                  <p class="fw-bold mb-0">
                    $90
                  </p>
                </div>
              </div>
              <div class="d-flex align-items-center mb-4">
                <div class="flex-shrink-0">
                  <img
                    src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-profiles/avatar-2.webp"
                    alt="Generic placeholder image"
                    class="img-fluid rounded-circle border border-dark border-3"
                    style="width: 70px"
                  >
                </div>
                <div class="flex-grow-1 ms-3">
                  <div class="d-flex flex-row align-items-center mb-2">
                    <p class="mb-0 me-2">
                      {{ user.email }}
                    </p>
                    <ul
                      class="mb-0 list-unstyled d-flex flex-row"
                      style="color: #1b7b2c"
                    >
                      <li>
                        <i class="fas fa-star fa-xs" />
                      </li>
                      <li>
                        <i class="fas fa-star fa-xs" />
                      </li>
                      <li>
                        <i class="fas fa-star fa-xs" />
                      </li>
                      <li>
                        <i class="fas fa-star fa-xs" />
                      </li>
                      <li>
                        <i class="fas fa-star fa-xs" />
                      </li>
                    </ul>
                  </div>
                  <div>
                    <button
                      type="button"
                      class="btn btn-outline-dark btn-rounded btn-sm"
                      data-mdb-ripple-color="dark"
                    >
                      + Follow
                    </button>
                    <button
                      type="button"
                      class="btn btn-outline-dark btn-rounded btn-sm"
                      data-mdb-ripple-color="dark"
                    >
                      See profile
                    </button>
                    <button
                      type="button"
                      class="btn btn-outline-dark btn-floating btn-sm"
                      data-mdb-ripple-color="dark"
                    >
                      <i class="fas fa-comment" />
                    </button>
                  </div>
                </div>
              </div>
              <hr>
              <p class="my-4 pb-1">
                52 comments
              </p>
              <button
                type="button"
                class="btn btn-success btn-rounded btn-block btn-lg"
              >
                <i class="far fa-clock me-2" />Book now
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
  name: 'ProfilePage',
  layout (context) {
    return 'CustomDefault'
  },
  data () {
    return {
      pengguna: []
    }
  },
  head () {
    return {
      link: [
        { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' },
        {
          rel: 'stylesheet',
          href: 'https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css'
        },
        {
          rel: 'stylesheet',
          href: 'https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons'
        },
        {
          rel: 'stylesheet',
          href: 'https://maxcdn.bootstrapcdn.com/font-awesome/latest/css/font-awesome.min.css'
        },
        {
          rel: 'stylesheet',
          href: 'https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Roboto+Slab:400,700|Material+Icons'
        }
      ],
      scripts: [
        {
          src: 'https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js',
          body: true
        },
        {
          src: 'https://unpkg.com/popper.js@1.12.6/dist/umd/popper.js',
          body: true
        },
        {
          src: 'https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js',
          body: true
        },
        {
          src: 'https://unpkg.com/bootstrap-material-design@4.1.1/dist/js/bootstrap-material-design.js',
          body: true
        }
      ]
    }
  },
  computed: {},
  mounted () {
    console.log('user-profile: ', this.pengguna)
    this.getProfilePengguna()
  },
  methods: {
    async getProfilePengguna () {
      try {
        await this.$axios
          .$get('https://jylpaciooxarhelwslji.supabase.co/rest/v1/pengguna', {
            headers: {
              apikey:
                'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imp5bHBhY2lvb3hhcmhlbHdzbGppIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTU3MjIxODYsImV4cCI6MjAxMTI5ODE4Nn0.DxbkTiy25jW5QSd3FgEvZm2G21JzU9kbcBSCdkOvmrU'
            }
          })
          .then((res) => {
            res.map(data => this.pengguna.push(data))
          })
      } catch (e) {
        console.log(e)
      }
    }
  }
}
</script>
