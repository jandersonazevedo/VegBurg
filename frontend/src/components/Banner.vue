<template>
  <div id="main-banner">
    <h1>Make Your Veggie Burger!</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("../../public/img/burger.jpg");
  background-position: center;
  background-size: cover;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

h1 {
    color: white;
    text-align: center;
    font-size: 30px;
    background-color: rgba(17, 17, 17, 0.411);
    padding: 20px 40px;
    backdrop-filter: blur(10px);
    font-weight: 400;
    border-radius: 0px 4px 4px 0px;
}
</style>