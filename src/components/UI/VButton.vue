<template>
  <div class="register-button">
    <button
      class="register-button__btn"
      :class="disabledButton"
      :disabled="!fieldsRequired"
      type="submit"
    >
      Зарегистрироваться
    </button>
  </div>
</template>

<script>
export default {
  name: "VButton",
  props: {
    fieldsRequired: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    disabledButton() {
      return {
        "register-button__btn_disabled": !this.fieldsRequired,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.register-button {
  display: flex;
  &__btn {
    width: 100%;
    padding: 16px 0px 16px;
    border: 2px solid transparent;
    border-radius: 6px;

    font-size: 16px;
    font-weight: 500;
    color: #fff;

    background: #0880ae;
    box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
      0px 4px 8px rgba(44, 39, 56, 0.08);

    transition: box-shadow 0.2s linear;
    &:hover:not(&_disabled) {
      box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.08),
        0px 24px 48px rgba(44, 39, 56, 0.16);
    }
    &:active {
      border: 2px solid rgba(44, 39, 56, 0.86);
    }
    &_disabled {
      background: #dbe2ea;
      cursor: not-allowed;
    }
  }
}
</style>
