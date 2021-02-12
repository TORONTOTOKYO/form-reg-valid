<template>
  <div class="have-account">
    <div class="have-account__text">Уже есть аккаунт?</div>
    <a href="#" class="have-account__link">Войти</a>
  </div>
</template>

<script>
export default {
  name: "HaveAccount",
};
</script>

<style lang="scss" scoped>
.have-account {
  display: flex;
  font-size: 16px;
  font-weight: 400;
  &__text {
    margin-right: 6px;

    line-height: 1.3;
  }
  &__link {
    color: #0880ae;

    line-height: 1.3;
    &:hover {
      color: #0aa1dd;
    }
  }
}
</style>
