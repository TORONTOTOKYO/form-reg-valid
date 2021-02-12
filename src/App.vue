<template>
  <div id="app">
    <div class="container">
      <Form />
    </div>
  </div>
</template>

<script>
import Form from "@/components/Form";
export default {
  name: "App",
  components: {
    Form,
  },
  data() {
    return {
      closedDropDown: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  max-width: 568px;
  margin: 50px auto 50px;
  padding: 20px;
}
</style>
