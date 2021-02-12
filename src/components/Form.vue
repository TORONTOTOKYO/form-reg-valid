<template>
  <form class="form" @submit.prevent="onSubmit" novalidate>
    <h1 class="form__title">Регистрация</h1>
    <Have-account class="form__have-account" />

    <V-input
      v-model.trim="$v.user.name.$model"
      :value="user.name"
      class="form__item"
      LabelTitle="Имя"
      InputPlaceholder="Введите ваше имя"
      Type="text"
      :validation="$v.user.name.alpha"
    />
    <V-input
      v-model.trim="$v.user.email.$model"
      :value="user.email"
      class="form__item"
      LabelTitle="Email"
      InputPlaceholder="Введите ваш Email"
      Type="email"
      :validation="$v.user.email.email"
    />
    <V-input
      v-model.trim="$v.user.phone.$model"
      :value="user.phone"
      class="form__item"
      LabelTitle="Номер телефона"
      InputPlaceholder="Введите ваш номер телефона"
      Type="text"
      :validation="$v.user.phone.checkNumber"
    />
    <V-dropdown
      class="form__dropdown"
      :langs="lang"
      :currentLang="user.lang"
      @select-lang="selectLang"
    />
    <V-checkbox
      Type="checkbox"
      class="form__checkbox"
      v-model.trim="$v.user.aceptedTerms.$model"
      :value="user.aceptedTerms"
    />
    <V-button :fieldsRequired="fieldsRequired" />
  </form>
</template>

<script>
const {
  required,
  sameAs,
  email,
  helpers,
} = require("vuelidate/lib/validators");

const alpha = helpers.regex("alpha", /^[а-яА-Я\s*-]+$/);
const checkNumber = helpers.regex(
  "checkNumber",
  /^\+?[78][(]?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$/
);

import HaveAccount from "@/components/HaveAccount";
import VInput from "@/components/UI/VInput";
import VDropdown from "@/components/UI/VDropdown";
import VCheckbox from "@/components/UI/VCheckbox";
import VButton from "@/components/UI/VButton";

export default {
  name: "Form",
  components: {
    HaveAccount,
    VInput,
    VDropdown,
    VCheckbox,
    VButton,
  },

  data() {
    return {
      user: {
        name: "",
        email: "",
        phone: "",
        lang: "",
        aceptedTerms: "",
      },
      lang: ["Русский", "Английский", "Китайский", "Испанский"],
    };
  },
  methods: {
    selectLang(lang) {
      this.user.lang = lang;
    },
    onSubmit(event) {
      console.log("Пользователь создан успешно и отправлен на сервер : )");
      event.target.reset();

      for (let key in this.user) {
        this.user[key] = "";
      }
    },
  },
  computed: {
    fieldsRequired() {
      return (
        !this.$v.user.$error && this.$v.user.$dirty && this.user.lang !== ""
      );
    },
  },

  validations: {
    user: {
      name: {
        required,
        alpha,
      },
      email: {
        required,
        email,
      },
      phone: {
        required,
        checkNumber,
      },
      aceptedTerms: {
        required,
        sameAs: sameAs(() => true),
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.form {
  width: 100%;
  max-width: 460px;
  height: 789px;
  margin: 0 auto;
  padding: 40px 30px 0px;
  border-radius: 24px;
  background: #fff;
  box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02),
    0px 32px 64px rgba(44, 39, 56, 0.04);
}
.form__title {
  margin-bottom: 10px;
  font-size: 34px;
  font-weight: 700;
}
.form__have-account {
  margin-bottom: 56px;
}
.form__item {
  margin-bottom: 44px;
}
.form__dropdown {
  margin-bottom: 35px;
}
.form__checkbox {
  margin-bottom: 40px;
}
@media (max-width: 568px) {
  .form {
    &__title {
      font-size: 30px;
    }
  }
}
</style>
