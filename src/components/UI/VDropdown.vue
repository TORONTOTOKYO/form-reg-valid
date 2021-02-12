<template>
  <div class="dropdown">
    <label class="dropdown__label" for="dropdownShow">Язык</label>
    <input
      type="text"
      readonly
      class="dropdown__show"
      id="dropdownShow"
      :value="changeLang"
      :class="{ isActiveTextinMenu: fieldHasBeenAffected, isActive: isOpen }"
      @click="showDropDownMenu"
      @blur="closeMenu"
    />

    <div class="dropdown__hidden" v-if="isOpen">
      <div
        class="dropdown__hidden-item"
        v-for="(item, index) in langs"
        :key="index"
        @click="() => selectLang(item)"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "VDropdown",
  props: {
    currentLang: {
      type: String,
      required: true,
    },
    langs: {
      type: Array,
      required: true,
    },
  },

  data() {
    return {
      isOpen: false,
    };
  },

  methods: {
    closeMenu() {
      window.setTimeout(() => {
        this.isOpen = false;
      }, 100);
    },
    showDropDownMenu() {
      this.isOpen === false ? (this.isOpen = true) : (this.isOpen = false);
    },
    selectLang(lang) {
      this.isOpen = false;
      this.$emit("select-lang", lang);
    },
  },
  computed: {
    changeLang() {
      return this.currentLang === "" ? "Язык" : this.currentLang;
    },
    fieldHasBeenAffected() {
      return this.currentLang === "";
    },
  },
};
</script>

<style lang="scss" scoped>
.dropdown {
  position: relative;
  &__label {
    display: block;
    margin-bottom: 7px;

    color: #2c2738;
    &::after {
      content: "";
      position: absolute;
      display: block;
      top: 50%;
      right: 20px;
      z-index: 1;
      pointer-events: none;
      width: 14px;
      height: 14px;
      border-bottom: 2px solid #0880ae;
      border-right: 2px solid #0880ae;

      transform: rotate(44deg);
    }
  }
  &__show {
    width: 100%;
    padding: 16px 0px 15px 16px;
    border: 1px solid #dbe2ea;
    border-radius: 6px;

    font-size: 16px;
    font-weight: 400;
    color: #2c2738;

    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);

    cursor: pointer;
  }
  &__hidden {
    position: absolute;

    z-index: 100;
    top: 105%;
    width: 100%;
    padding: 10px 0px 11px 0px;
    border: 1px solid #dbe2ea;
    border-radius: 6px;
    background: #fff;

    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04),
      0px 20px 20px rgba(44, 39, 56, 0.04);
  }
  &__hidden-item {
    padding: 10px 0px 11px 15px;
    color: #2c2738;
    transition: background 0.2s linear;
    cursor: pointer;

    &:hover {
      background: #ebf4f8;
    }
  }
  .isActive {
    border: 2px solid #0880ae;
  }
  .isActiveTextinMenu {
    color: #7c9cbf;
  }
}
</style>
