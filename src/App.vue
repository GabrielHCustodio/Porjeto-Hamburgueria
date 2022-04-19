<template>
  <NavbarHamb :logo="logo_src" :alt="name_app"/>
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
  },
  data() {
    return {
      logo_src: "/image/logo.png",
      name_app: "Make your burguer"
    }
  }
}
</script>

<style>
  * {
    font-family: Helvetica;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }

</style>
