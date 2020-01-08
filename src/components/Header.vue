<template>
  <header>
      <div class="navbar navbar-default">
          <h1>
            <router-link :to="{name: 'iMain'}">
              {{ sitename }}
            </router-link>
          </h1>
      </div>
      <div class="nav navbar-nav cart navbar-right">
        <router-link
          active-class="active"
          tag="button"
          class="btn btn-default btn-lg"
          :to="{name: 'Form'}">
          <span
              class="glyphicon glyphicon-shopping-cart"
          >{{ cartItemCount }}</span>
          Checkout
        </router-link>
      </div>
  </header>
</template>

<script>
export default {
  name: "my-header",
  data(){
    return {
      sitename: "Vejs petshop"
    }
  },
  props: ["cartItemCount"],
  methods: {
    showCheckout() {
      this.$router.push({name: "Form"})
    }
  }
}
</script>

<style scoped>
a {
  text-decoration: none;
  color: black;
}
.router-link-exact-active {
  color: blue;
}
</style>