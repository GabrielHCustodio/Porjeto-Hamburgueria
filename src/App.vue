<template>
  <NavbarHamb />
  <router-view/>
  <FooterHamb />
</template>

<script>
import NavbarHamb from "./components/Navbar.vue"
import FooterHamb from "./components/Footer.vue"

export default {
  components: {
    NavbarHamb,
    FooterHamb
  }
}
</script>

<style>

</style>
