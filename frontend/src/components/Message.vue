<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.message-container {
  color: #007e39;
  background-color: #ccfde2;
  border: 2px solid #b2e7ca;
  border-radius: 4px;
  padding: 10px;
  max-width: 400px;
  margin: 30px auto;
}
</style>
