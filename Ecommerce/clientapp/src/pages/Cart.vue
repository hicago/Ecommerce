<template>
  <b-container class="pt-4 page">
    <h1 class="pb-4">Shopping cart</h1>
    <p v-if="!items.length" class="mt-4 text-center">
      You don't have anything in your cart yet!
    </p>
    <div v-else class="table-responsive">
      <table class="table">
        <thead>
          <tr>
            <th>Product</th>
            <th>Price</th>
            <th>Quantity</th>
            <th>Subtotal</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <cart-item v-for="(item, index) in items" :key="index" :item="item" />
        </tbody>
        <tfoot>
          <tr>
            <td>
              <b-button variant="secondary" @click="continueShopping">
                <!-- <i class="fas fa-chevron-left"></i> -->
                <font-awesome-icon icon="chevron-left" />
                Continue shopping
              </b-button>
            </td>
            <td colspan="2"></td>
            <td>
              <strong>Total: {{ total | currency }}</strong>
            </td>
            <td>
              <b-button variant="success" @click="checkout">
                Check out
                <font-awesome-icon icon="chevron-right" />
              </b-button>
            </td>
          </tr>
        </tfoot>
      </table>
    </div>
  </b-container>
</template>

<script>
import CartItem from "../components/cart/CartItem.vue";
export default {
  name: "cart",
  components: {
    CartItem,
  },
  computed: {
    items: function() {
      return this.$store.state.cart;
    },
    total: function() {
      return this.$store.getters.shoppingCartTotal;
    },
  },
  methods: {
    continueShopping() {
      this.$router.go(-1);
    },
    checkout() {
      this.$router.push("/checkout");
    },
  },
};
</script>
