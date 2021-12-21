<template>
  <div class="checkout__wrapper container">
    
    <div class="row bg-theme pb-4">
      <div class="col-12 d-flex pt-3">
        <img class="rounded-pill" src="https://picsum.photos/30" alt="">
        <div class="ms-auto fw-bold text-danger cursor-pointer" data-bs-toggle="modal" data-bs-target="#myModal">
          View Order
        </div>
      </div>

      <div class="col-12 d-flex pt-3">
        <div>
          Arrow Shop
        </div>
        <div class="ms-auto fw-bold">
          <h5>$ {{total}} </h5>
        </div>
      </div>

      
      
    </div>
    <div class="row p-2 bg-white">
      <div class="col-12 p-0 text-uppercase">
        Billing Details
      </div>
      <div class="col-12 p-0 border border-bottom-0 border-rounded-top-80 d-flex">
          <vue-country-code
                  class="border-0 px-2"
                  @onSelect="onSelect"
                  :preferredCountries="['vn', 'us', 'gb']">
          </vue-country-code>

          <input v-model="order.phone" type="number" class="form-control shadow-none rounded-pill py-3 border-0" id="phone" placeholder="Phone number" name="phone">
      </div>
      <div class="col-6 p-0 border border-end-0 ">
          <input v-model="order.first_name" type="text" class="form-control shadow-none rounded-pill py-3 border-0" id="first_name" placeholder="First Name" name="first_name">
      </div>
      <div class="col-6 p-0 border">
          <input v-model="order.last_name" type="text" class="form-control shadow-none rounded-pill py-3 border-0" id="last_name" placeholder="Last Name" name="last_name">
      </div>
      <div class="col-12 p-0 border border-rounded-bottom-80">
          <input v-model="order.email" type="email" class="form-control shadow-none rounded-pill py-3 border-0" id="email" placeholder="Email" name="email">
      </div>
      
      
    </div>

    <div class="row p-2">
      <div class="col-12 p-0 border border-rounded-top-80 border-rounded-bottom-80 d-flex">
          <vue-country-code
                  class="border-0 px-2"
                  @onSelect="onSelect"
                  :preferredCountries="['vn', 'us', 'gb']">
          </vue-country-code>

          <input v-model="order.address" type="text" class="form-control shadow-none rounded-pill py-3 border-0" id="address" placeholder="Address" name="address">
      </div>
    </div>

    <div class="row mb-3 p-2 ">
      <div class="col-12 p-0 text-uppercase">
        Payment Method
      </div>

      <div class="col-12 p-0">
        <select v-model="order.payment_mode" class="form-select p-2 px-3 border-rounded-top-80 border-rounded-bottom-80">
          <option value="Card">💳 Card</option>
          <option value="PayNow">💳 PayNow</option>
        </select>
      </div>
    </div>


    <div class="row mb-3 p-2" v-if="order.payment_mode == 'Card'">
      <div class="col-12 p-0 border border-bottom-0 border-rounded-top-80">
          <input v-model="order.card.number" type="number" class="form-control shadow-none rounded-pill py-3 border-0" id="card_number" placeholder="Enter card number" name="card_number">
      </div>
      <div class="col-6 p-0 border border-end-0 border-rounded-bottom-left-80">
          <input v-model="order.card.expiry_date" type="text" class="form-control shadow-none rounded-pill py-3 border-0" id="expiry_date" placeholder="Expiry date" name="expiry_date">
      </div>
      <div class="col-6 p-0 border border-rounded-bottom-right-80">
          <input v-model="order.card.cvv" type="text" class="form-control shadow-none rounded-pill py-3 border-0" id="cvv" placeholder="CVV" name="cvv">
      </div>
    </div>

    
    <div class="d-grid mb-2">
      <button class="btn shadow-sm btn-dark btn-block p-3 text-uppercase text-white-50 border-rounded-top-80 border-rounded-bottom-80">
        Confirm & Pay
        <svg fill="#901643" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M8.122 24l-4.122-4 8-8-8-8 4.122-4 11.878 12z"/></svg>
      </button>
    </div>

    <!-- modal to show cart items -->
    <CartViewModal :total="total" :totalDiscount="totalDiscount" :items="order.items"/>
  </div>
</template>

<script>
import CartViewModal from "./CartViewModal.vue"
export default {
  name: 'Checkout',
  components: {
    CartViewModal
  },
  data() {
    return {
      order: {
        first_name: "",
        last_name: "",
        email: "",
        phone: "",
        address: "",
        payment_mode: "Card",
        card: {
          number: "",
          expiry_date: "",
          cvv: ""
        },
        items: [
          {id: 1, name: "Binachi Bicycle model eagle", mrp: 218, price: 200, qty: 1},
          {id: 2, name: "T-Shirt black", mrp: 118, price: 100, qty: 2},
          {id: 3, name: "100% Hypercraft Sunglasses", mrp: 213, price: 193, qty: 1}
        ]


      }
    }
  },

  computed: {
    total: function() {
       return this.order.items.reduce( (total, item) => {
          return total + item.price
        }, 0)
    },
    totalDiscount: function() {
       return this.order.items.reduce( (total, item) => {
          return total + (item.mrp-item.price)
        }, 0)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-theme {
  background: #f6f6f6;
}

.border-rounded-top-80 {
  border-top-left-radius: 0.80rem!important;
  border-top-right-radius: 0.80rem!important;
}
.border-rounded-bottom-80 {
  border-bottom-left-radius: 0.80rem!important;
  border-bottom-right-radius: 0.80rem!important;
}
.border-rounded-bottom-right-80 {
  border-bottom-right-radius: 0.80rem!important;
}
.border-rounded-bottom-left-80 {
  border-bottom-left-radius: 0.80rem!important;
}
</style>
