<template>
  <section class="vh-100" style="background-color: #eee;">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-md-12 col-xl-4">
          <div class="card" style="border-radius: 15px;">
            <div class="card-body text-center">
              <div class="mt-3 mb-4">
                <img
                  src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-chat/ava2-bg.webp"
                  class="rounded-circle img-fluid"
                  style="width: 100px;"
                >
              </div>
              <h4 class="mb-2">
                {{ loggedInUser.username }}
              </h4>
              <p class="text-muted">
                Status <span class="mx-2">:</span>{{ isAuthenticated ? 'Login' : 'Logout' }}
              </p>
              <p class="text-muted mb-4">
                Email<span class="mx-2">:</span> <a
                  href="#!"
                ><strong>{{ loggedInUser.email }}</strong></a>
              </p>
              <!-- <div class="mb-4 pb-2">
              <button type="button" class="btn btn-outline-primary btn-floating">
                <i class="fab fa-facebook-f fa-lg"></i>
              </button>
              <button type="button" class="btn btn-outline-primary btn-floating">
                <i class="fab fa-twitter fa-lg"></i>
              </button>
              <button type="button" class="btn btn-outline-primary btn-floating">
                <i class="fab fa-skype fa-lg"></i>
              </button>
            </div> -->
              <button type="button" class="btn btn-primary btn-rounded btn-lg">
                Ayo liat-liat aja dulu!
              </button>
            <!-- <div class="d-flex justify-content-between text-center mt-5 mb-2">
              <div>
                <p class="mb-2 h5">8471</p>
                <p class="text-muted mb-0">Wallets Balance</p>
              </div>
              <div class="px-3">
                <p class="mb-2 h5">8512</p>
                <p class="text-muted mb-0">Income amounts</p>
              </div>
              <div>
                <p class="mb-2 h5">4751</p>
                <p class="text-muted mb-0">Total Transactions</p>
              </div>
            </div> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- <section class="vh-100" style="background-color: #eee">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col col-md-9 col-lg-7 col-xl-5">
          <div
            class="card"
            style="border-radius: 15px; background-color: #93e2bb"
          >
            <div
              class="card-body p-4 text-black"
            >
              <div>
                <h6 class="mb-4">
                  Profile
                </h6>
                <div
                  class="d-flex align-items-center justify-content-between mb-3"
                >
                  <p class="small mb-0">
                    <strong>Status: </strong>{{ isAuthenticated ? 'Login' : 'Logout' }}
                  </p>
                </div>
              </div>
              <div class="d-flex align-items-center mb-4">
                <div class="flex-shrink-0">
                  <img
                    src="https://images.pexels.com/photos/5537575/pexels-photo-5537575.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
                    alt="Generic placeholder image"
                    class="img-fluid rounded-circle border border-dark border-3"
                    style="width: 70px"
                  >
                </div>
                <div class="flex-grow-1 ms-3">
                  <div class="d-flex flex-row align-items-center mb-2">
                    <p class="mb-0 me-2">
                      <Strong>User Name: </Strong>{{ loggedInUser.username }}
                    </p>
                    <p class="mb-0 me-2">
                      <strong>Your Email: </strong>{{ loggedInUser.email }}
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
                <strong>Status: </strong>{{ isAuthenticated ? 'Login' : 'Logout' }}
              </p>
              <button
                type="button"
                class="btn btn-success btn-rounded btn-block btn-lg"
              >
                <i class="far fa-login me-2" />Belanja Sekarang!
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <div class="container">
      <h2 class="title">
        My Profile
      </h2>
      <div class="content">
        <p>
          <strong>Username:</strong>
          {{ loggedInUser.username }}
        </p>
        <p>
          <strong>Email:</strong>
          {{ loggedInUser.email }}
        </p>
        <p>
          <strong>Status:</strong>
          {{ isAuthenticated }}
        </p>
      </div>
    </div>
  </section> -->
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  layout (context) {
    return 'CustomDefault'
  },
  middleware: 'auth',
  computed: {
    ...mapGetters(['loggedInUser', 'isAuthenticated'])
  }
}
</script>
