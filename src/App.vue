<template>
 <header class="top-bar spread">
        <nav class="top-bar-nav">
          <router-link to="/" class="top-bar-link">
            <span>Trang chủ</span>
          </router-link>
          <router-link to="/products" class="top-bar-link">
            <span>Tất cả sản phẩm</span>
          </router-link>
        </nav>
        <div @click="toggleSidebar" class="top-bar-cart-link">
          <i class="icofont-cart-alt icofont-1x"></i>
          <span>Giỏ hàng ({{totalQuantity}})</span>
        </div>
  </header>
  <router-view :inventory="inventory" :addToCart="addToCart"/>
  <footer ><span >ĐỒ ÁN CHUYÊN NGÀNH</span></footer>
  <Sidebar
        v-if="showSidebar"
        :toggle="toggleSidebar"
        :cart="cart"
        :inventory="inventory"
        :remove="removeItem"
  />
</template>
<script>
import Sidebar from './components/Sidebar.vue'
import food from './food.json'
export default {
  components: {
    Sidebar
  },
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (name) {
      delete this.cart[name]
    }
  }
}
</script>
