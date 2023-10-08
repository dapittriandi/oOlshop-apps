<template>
  <section class="section">
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
  </section>
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
