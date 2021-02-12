<template>
  <div class="checkbox">
    <input
      :type="Type"
      class="checkbox__input"
      id="checkboxAccept"
      :value="value"
      @input="$emit('input', $event.target.checked)"
    />
    <label for="checkboxAccept" class="checkbox__label"
      ><span
        >Принимаю
        <a class="checkbox__link" href="#"> условия </a> использования</span
      ></label
    >
  </div>
</template>

<script>
export default {
  name: "VCheckbox",
  props: {
    value: {
      type: Boolean,
      required: true,
    },
    Type: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.checkbox {
  &__input {
    display: none;

    &:checked + .checkbox__label::before {
      border: 2px solid #0880ae;
    }
    &:checked + .checkbox__label::after {
      opacity: 1;
    }
  }
  &__label {
    position: relative;

    display: flex;
    align-items: center;
    line-height: 140%;
    font-size: 16px;
    font-weight: 500;
    color: #756f86;

    cursor: pointer;
    &::before {
      content: "";
      flex: 0 0 28px;
      align-self: center;
      height: 28px;
      margin-right: 10px;

      border: 1px solid #dbe2ea;
      border-radius: 6px;

      box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    }
    &::after {
      content: "";

      position: absolute;
      left: 10px;
      top: 4px;
      width: 9px;
      height: 15px;
      border: solid #0880ae;
      border-width: 0 2px 2px 0;
      transform: rotate(45deg);
      opacity: 0;

      transition: opacity 0.2s linear;
    }
  }
  &__link {
    color: #0880ae;
    &:hover {
      color: #0aa1dd;
    }
  }

  @media (max-width: 568px) {
    .checkbox {
      &__label {
        font-size: 13px;
      }
    }
  }
}
</style>
