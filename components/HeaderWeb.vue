<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand" href="/">Bumi Style</a>
      <b-navbar-toggle target="nav-collapse" />
      <b-collapse id="nav-collapse" is-nav>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <a class="nav-link" href="/">Home</a>
          </li>
          <li class="nav-item">
            <div class="navbar-item has-dropdown is-hoverable">
              <a
                class="navbar-link"
                href="/app/product"
                style="
                  border-radius: 10px;
                  text-decoration: none;
                  font-family: 'Roboto Condensed', sans-serif;
                  color: #000;
                "
              >Product</a>
              <div class="navbar-dropdown">
                <nuxt-link class="navbar-item" to="/add-product">
                  Product Check
                </nuxt-link>
                <nuxt-link class="navbar-item" to="/app/form/add-product">
                  Add Product
                </nuxt-link>
                <nuxt-link class="navbar-item" to="/app/form/add-product">
                  tambah
                </nuxt-link>
                <hr class="navbar-divider">
                <a class="navbar-item" href="/app/cart/">cart</a>
              </div>
            </div>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/history">History</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/about">About</a>
          </li>

          <div
            v-if="isAuthenticated"
            class="navbar-item has-dropdown is-hoverable"
            style="
              margin-left: 2px;
              font-family: 'Roboto Condensed', sans-serif;
              color: #000;
            "
          >
            <a class="navbar-link" style="border-radius: 10px; color: #000">
              {{ loggedInUser.username }}
              <i
                class="fas fa-user"
                style="color: #3877ff; margin-left: 7px; font-size: 20px"
              /></a>
            <div class="navbar-dropdown">
              <nuxt-link class="navbar-item" to="/profile">
                My Profile
              </nuxt-link>
              <hr class="navbar-divider">
              <a class="navbar-item" @click="logout">Logout</a>
            </div>
          </div>

          <template v-else>
            <li class="nav-item" style="margin-top: 8px">
              <nuxt-link class="login" role="button" to="/login">
                login
              </nuxt-link>
              <nuxt-link class="register" role="button" to="/register">
                Daftar
              </nuxt-link>
            </li>
          </template>
        </ul>
      </b-collapse>
    </div>
  </nav>
</template>
<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['isAuthenticated', 'loggedInUser'])
  },
  methods: {
    async logout () {
      await this.$auth.logout()
    }
  }
}
</script>

<style scoped>
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-family: 'Merriweather Sans', sans-serif;
  padding: 20px 0;
  background-color: rgba(209, 209, 209, 0.305) !important;
  backdrop-filter: saturate(180%) blur(20px);
  -webkit-backdrop-filter: saturate(180%) blur(20px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.185);
  z-index: 999;
  position: sticky;
  /* opacity: 0.9; */
  top: 0;
  left: 0;
}

.navbar-brand {
  font-size: 21px;
  font-weight: 600;
  font-family: 'Merriweather Sans', sans-serif;
}

.nav-item {
  font-size: 16px;
  font-family: 'Roboto Condensed', sans-serif;
}

.navbar-light .nav-link {
  color: rgb(0, 0, 0);
  transition-duration: 0.3s;
}

.navbar-light .nav-link:hover {
  color: #3877ff;
}

.login {
  font-size: 16px;
  border-radius: 10px;
  outline: none;
  padding: 6px 13px;
  text-decoration: none;
  color: #000000;
  transition: 0.5s;
}

.register {
  color: #fff;
  background-color: #3877ff;
  font-size: 16px;
  border-radius: 10px;
  margin-left: 2px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.359);
  padding: 7px 14px;
  text-decoration: none;
  transition: 0.5s;
}

.login:hover {
  background-color: transparent;
  border: 1px solid #000000;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.359);
  padding: 5px 12px;
}

.register:hover {
  background-color: transparent;
  color: #000000;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.359);
  border: 1px solid #000000;
  padding: 5px 12px;
}

@media (max-width: 799px) {
  .navbar {
    background-color: #e3e6f3;
  }
}
</style>
