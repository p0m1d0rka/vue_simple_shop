<template>
  <div>
    <my-header :cartItemCount="cartItemCount"></my-header>
    <main>
      <div v-for="product in sortedProducts" :key="product.id">
        <div class="row product">
          <div class="col-md-5 col-md-offset-0">
            <figure>
                <img class="product-min" v-bind:src="product.image">
            </figure>
          </div>                    
          <div class="col-md-5 col-expand">
            <router-link
              tag="h1"
              :to="{name: 'Id', params: {id: product.id}}">
              {{product.title}}
            </router-link>

            <p v-html="product.description"></p>
            <p class="price">{{ product.price }}</p>
            <button 
                class="btn btn-success"
                @click="addToCart(product)"
                v-if="canAddToCart(product)"
              >Add to cart
            </button>
            <button 
                class="btn disabled"
                v-else
              >Add to cart
            </button>
            <span 
                class="inventory-message"
                v-if="product.availableInventory - cartCount(product.id) == 0">
                All Out!
            </span>
            <span 
                class="inventory-message"
                v-else-if="product.availableInventory - cartCount(product.id) < 5">
                Only {{ product.availableInventory - cartCount(product.id) }} left!
            </span>
            <span 
                class="inventory-message"
                v-else>
                Buy Now!
            </span>
            <div class="rating">
                <span 
                    v-for="n in 5"
                    :key=n
                    v-bind:class="{'rating-active': checkRating(n, product)}"
                >&#9734;</span>
            </div>
          </div>   
        </div>
      </div>  
    </main>
  </div>
</template>

<script>
import MyHeader from "./Header"
export default {
  name: "imain",
  data() {
    return {
      products: {},
      cart: []
    }
  },
  components: { MyHeader },
  methods: {
  addToCart: function(product){
    console.log(`Call add to cart for ${product.id}`)
    this.cart.push( product.id )
  },
  showCheckout() {
    this.showProduct = !this.showProduct
  },
  checkRating(n, product) {
    return product.rating - n >=0
  },
  canAddToCart(product) {
    return product.availableInventory > this.cartCount(product.id)
  },
  cartCount(productId) {
    let count=0;
    for(var i=0; i< this.cart.length; i++) {
        if(this.cart[i] === productId){
            count++
        }
    }
    return count
   }  
  },
  filters: {},
  created: function() {
    axios.get("/static/products.json")
    .then(response => {
      this.products = response.data.products
      console.log(this.products)
    })
  },
  computed: {
    cartItemCount: function(){
        return this.cart.length || 0
    },
    sortedProducts: function(){
      if(this.products.length >0){
        let productsArray = this.products.slice(0)
        console.log(productsArray)
        function compare(a,b){
          if(a.title.toLowerCase() < b.title.toLowerCase()){
              return -1
          }
          if(a.title.toLowerCase() > b.title.toLowerCase()){
              return 1
          }
          return 0
        }
        return productsArray.sort(compare)
      }
      return this.products
    }
  },  
}
</script>