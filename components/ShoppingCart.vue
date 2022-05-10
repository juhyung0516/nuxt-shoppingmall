<template>
  <div>
    <div
      id="offcanvasRight"
      class="offcanvas offcanvas-end"
      tabindex="-1"
      aria-labelledby="offcanvasRightLabel"
    >
      <div class="offcanvas-header">
        <h5 id="offcanvasRightLabel">Shopping cart - $ {{ totalSum }}</h5>

        <button
          type="button"
          class="btn-close text-reset"
          data-bs-dismiss="offcanvas"
          aria-label="Close"
        ></button>
      </div>
      <div class="offcanvas-body">
        <div
          v-for="(product, index) in modelValue"
          :key="'cart-product-' + index"
          class="card mb-3"
        >
          <div class="row">
            <div class="col-md-4">
              <img :src="product.photoURL" class="img-fluid rounded-start" />
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">
                  {{ product.name }}
                </h5>
                <p class="card-text">
                  {{ product.description }}
                </p>
                <p class="card-text">
                  {{ product.price }} x $ {{ product.amount }}
                </p>
                <div class="d-grid">
                  <button
                    class="btn btn-outline-secondary"
                    @click="removeFromCart(product)"
                  >
                    Remove
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="js">
export default {
  // eslint-disable-next-line vue/require-prop-types
  props: ['modelValue'],

  computed: {
    totalSum() {
      /// Sums all the prices and returns a TOTAL price

      let sum = 0

      for (const product of this.modelValue) {
        sum += product.price * product.amount
      }

      return sum
    },
  },

  methods: {
    removeFromCart(product) {
      // Looks for the item in the shopping cart array
      // Then, substracts one to the amount or removes it

      const shoppingCart = this.modelValue
      const productIndex = shoppingCart.findIndex(
        (item) => item.uuid === product.uuid
      )

      shoppingCart[productIndex].amount -= 1

      if (shoppingCart[productIndex].amount < 1) {
        shoppingCart.splice(productIndex, 1)
      }

      this.$emit('update:modelValue', shoppingCart)
    },
  },
}
</script>
