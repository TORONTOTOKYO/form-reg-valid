<template>
  <div class="item">
    <label for="" class="item__label">{{ LabelTitle }}</label>
    <input
      :value="value"
      @input="$emit('input', $event.target.value)"
      :type="Type"
      class="item__input"
      :placeholder="InputPlaceholder"
    />
    <div class="error" v-if="validationFiled">
      Введено не корректное значение
    </div>
  </div>
</template>

<script>
export default {
  name: "VInput",
  props: {
    validation: {
      type: Boolean,
      default: false,
    },
    value: {
      type: String,
      required: true,
    },
    LabelTitle: {
      type: String,
      required: true,
    },
    InputPlaceholder: {
      type: String,
      required: true,
    },
    Type: {
      type: String,
      required: true,
    },
  },
  computed: {
    validationFiled() {
      return !this.validation;
    },
  },
};
</script>

<style lang="scss" scoped>
.item {
  position: relative;
  &__label {
    display: block;
    margin-bottom: 7px;
    font-size: 16px;
    font-weight: 500;
    color: #756f86;
  }
  &__input {
    width: 100%;
    height: 52px;
    padding-left: 16px;

    border: 1px solid #dbe2ea;
    border-radius: 6px;

    font-family: "IBM Plex Sans", sans-serif;
    // font-size: calc(14px +2 * (100vw / 568));
    font-size: 16px;

    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    &::placeholder {
      font-size: 16px;
      font-weight: 400px;
      color: #7c9cbf;
    }
    &:focus {
      border: 2px solid #0880ae;
    }
  }
}
.error {
  position: absolute;
  bottom: -20px;
  left: 0;
  color: #ff7171;
  font-size: 14px;
  font-weight: 400;
}
</style>
