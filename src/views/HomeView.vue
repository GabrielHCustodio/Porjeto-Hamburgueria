<template>
  <BannerApp />
  <div class="main-container">
    <h1>Home</h1>
    <BurgerForm />
  </div>
</template>

<script>
import BannerApp from "../components/Banner.vue"
import BurgerForm from "../components/Burger.vue"

export default {
  name: "HomeApp",
  components: {
    BannerApp,
    BurgerForm
  }
}
</script>
