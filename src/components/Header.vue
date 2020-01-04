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
          <button class="btn btn-default btn-lg"
              @click="showCheckout"
          >
          <span
              class="glyphicon glyphicon-shopping-cart"
          >{{ cartItemCount }}</span>
          Checkout
          </button>
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
</style>