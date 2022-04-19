<template>
    <div id="main-banner">
        <h1>Make your burger</h1>
    </div>
</template>

<script>
export default {
    name: "BannerApp"
}
</script>

<style scoped>
  #main-banner {
    background-image: url('/public/image/burger.jpg');
    background-position: 0 -250px;
    background-size: cover;
    background-repeat: no-repeat;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }
  #main-banner h1 {
    color: #FFF;
    text-align: center;
    font-size: 60px;
    background-color: #222;
    padding: 20px 40px;
  }
</style>