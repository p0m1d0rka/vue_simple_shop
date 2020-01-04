<template>
  <div>
    <my-header :cartItemCount="cartItemCount"></my-header>
    <div class="col-md-6">
        <strong>First name:</strong>
        <input v-model.trim.lazy="order.firstName" 
            class="form-control" />
    </div>
    <div class="col-md-6">
        <strong>Last name:</strong>
        <input v-model.trim.lazy="order.lastName" 
            class="form-control" />
    </div>                                     
    <div class="form-group">
        <div class="col-md-12">
            <strong>Address:</strong>
        </div>
        <div class="col-md-12">
            <input v-model.trim.lazy="order.address" class="form-control" />
        </div>
    </div>
    <div class="form-group">
        <div class="col-md-12">
            <strong>City:</strong>
        </div>
        <div class="col-md-12">
            <input v-model.trim.lazy="order.city" class="form-control" />
        </div>
    </div>    
    <div class="form-group">
        <div class="col-md-12">
            <strong>State:</strong>
            <select
                v-model="order.state"
                class="form-control"
            >
                <option disabled value="">State</option>
                <option 
                    v-for="(state, key) in states"
                    v-bind:value="state"
                    v-bind:key="key"
                >
                {{ key }}
                </option>

            </select>
        </div>
    </div>
    <div class="form-group">
        <div class="col-md-6 col-md-offset-4">
            <strong>Zip Postal Code:</strong>
            <input v-model.number="order.zip" class="form-control" />
        </div>
    </div>  
    <div class="form-group">
        <div class="col-md-6 boxes">
            <input 
                type="checkbox"
                id="gift"
                value="true"
                v-bind:true-value="order.sendGift"
                v-bind:false-value="order.dontSendGift"
                v-model="order.gift" />
            <label for="gift">Ship as gift?</label>
        </div>
    </div> 
    <div class="form-group">
        <div class="col-md-6 boxes">
            <input 
                type="radio"
                id="home"
                v-bind:value="order.home"
                v-model="order.method"
            />
            <label for="home">Home</label>
            <input 
                type="radio"
                id="business"
                v-bind:value="order.business"
                v-model="order.method"
            />
            <label for="business">Business</label>
        </div> 
    </div>                      
    <div class="col-md-12 verify">
        <pre>
            First Name: {{ order.firstName }}
            Last Name: {{ order.lastName }}
            Address: {{ order.address }}
            City: {{ order.city }}
            Zip: {{ order.zip }}
            State: {{ order.state }}
            Method: {{ order.method }}
            Gift: {{ order.gift }}
        </pre>
    </div>    
    <div class="form-group">
        <div class="col-md-6">
            <button 
                type="submit"
                class="btn btn-primary submit"
                @click="submitForm"
            >Place Order</button>
        </div>
    </div>        
  </div>
</template>

<script>
import MyHeader from "./Header"
export default {
  name: "Form",
  props: ['cartItemCount'],
  data () {
    return {
      states: {
          AL: "Alabama",
          AR: "Arizona",
          CA: "California",
          NV: "Nevada"
      },
      order: {
          lastName: '',
          firstName: '',
          address: '',
          city: '',
          zip: '',
          state: '',
          method: 'Home address',
          home: 'Home address',
          business: 'Business address',
          gift: "Send as gift",
          sendGift: "Send as gift",
          dontSendGift: "So not send as a gift"
      }
    }
  },
  components: { MyHeader },
  methods: {
    submitForm(){
      alert("submitted")
    }
  }
}
</script>