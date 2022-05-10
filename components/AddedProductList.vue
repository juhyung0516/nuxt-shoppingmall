<template>
  <div id="addedproductlist">
    <div>
      <div>
        <div
          v-if="$store.getters.getcartProducts.length === 0"
          class="shopped-item"
        >
          장바구니에 담은 상품이 없습니다.
        </div>
        <div
          v-for="(cartproduct, index) in $store.getters.getcartProducts"
          v-else
          :key="index"
          class="shopped-item"
        >
          <div class="shopped-imgtitle">
            <img src="../assets/images/dogfood.jpg" />
            <div class="shopped-title">{{ cartproduct.title }}</div>
          </div>
          <div id="editquantity">
            <button @click="subOrder(cartproduct)">-</button>
            <div>
              {{ cartproduct.quantity }}
            </div>
            <button @click="addOrder(cartproduct)">+</button>
          </div>
          <div class="shopped-price">{{ cartproduct.itemtotalprice }}원</div>
        </div>
        <div class="shopped-total">
          총 가격 : {{ $store.getters.cartTotal }}원
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddedProductList',
  methods: {
    addOrder(cartproduct) {
      this.$store.dispatch('addOrder', cartproduct)
    },
    subOrder(cartproduct) {
      this.$store.dispatch('subOrder', cartproduct)
    },
  },
}
</script>
