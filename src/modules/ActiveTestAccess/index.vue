<template>
  <div class="modal">
    <div class="modal__header">Активация тестового доступа</div>
    <div class="modal__body">
      <div class="modal__description">
        Для активации 14-дневного тестового доступа заполните форму ниже.
      </div>
      <div class="modal__warning">
        <span class="important"> Внимание! </span>
        В целях безопасности обслуживание будет осуществляться только по
        указанному номеру телефона.
      </div>
      <div class="modal__form">
        <div class="modal__phone">
          <SelectForm
            :style="{ border: errorPhone }"
            class="modal__phone-select"
            :title="'Страна'"
            :options="countryNumbers"
            ref="number"
          />
          <input
            class="modal__phone-input input-form"
            type="text"
            placeholder="Введите номер телефона*"
            v-model="phone"
            ref="number"
          />
        </div>
        <input
          class="modal__name input-form"
          placeholder="Как к вам обращаться?*"
          ref="name"
        />
        <SelectForm
          :style="{ border: errorRole }"
          :options="roles"
          :placeholder="'Ваша роль в компании?*'"
          @selectOptions="selectOptions"
        />
      </div>
      <div class="modal__check check">
        <input type="checkbox" checked="true" value="true" name="'KEdmke'" />
        <label>Хочу получить бесплатную помощь в настройке</label>
      </div>
      <div class="modal__check check">
        <div class="check__body">
          <input
            type="checkbox"
            v-model="name"
            :checked="havePromocode"
            @click="togglePromocode()"
          />
          <span>У меня есть промокод</span>
        </div>
        <input
          class="modal__check-promocode input-form"
          type="text"
          v-show="havePromocode"
          ref="test"
          autofocus
          placeholder="Введите промокод"
        />
      </div>
      <button class="modal__btn button-form" @click="checkInputs()">
        Активировать доступ
      </button>
      <div class="modal__link">
        Есть вопросы? <span class="important">Напишите нам!</span>
      </div>
    </div>
  </div>
</template>

<script>
import SelectForm from "../../components/SelectForm.vue";

export default {
  data() {
    return {
      roles: [
        "Собственник",
        "Руководитель отдела продаж",
        "Технический специалист",
        "Интегратор amoSRM",
      ],
      countryNumbers: ["+7", "+68", "+1"],
      phone: "",
      name: "",
      role: "",
      promocode: "",
      havePromocode: false,
      errorPhone: "",
      errorRole: "",
    };
  },
  components: {
    SelectForm,
  },
  methods: {
    togglePromocode() {
      this.havePromocode = !this.havePromocode;
      this.$nextTick(() => this.$refs.test.focus());
    },

    selectOptions(v) {
      this.role = v;
    },

    checkInputs() {
      if (!this.phone) {
        this.$refs.number.style.border = "1px solid red";
        this.errorPhone = "1px solid red";
      }
      if (!this.name) this.$refs.name.style.border = "1px solid red";
      if (!this.role) this.errorRole = "1px solid red";
    },
  },
};
</script>

<style lang="sass" scoped>
$base-color: #BACBCE
$second-color: #E8EEEF
$radius: 4px
$accent-color: #17505B

input:active
  border: 1px solid $accent-color

.important
    font-weight: 500
    color: $accent-color

.modal
    width: 500px
    border: 1px solid $base-color
    display: flex
    justify-content: center
    flex-direction: column

    &__header
        width: 100%
        height: 64px
        display: flex
        justify-content: center
        align-items: center
        background-color: $base-color
        font-size: 24px
        font-weight: 500

    &__body
        padding: 36px 30px

    &__description
        margin-bottom: 30px
        font-size: 16px
        font-weight: 500
        line-height: 22px

    &__warning
        padding: 10px
        border-radius: $radius
        font-size: 12px
        background-color: $second-color
        color: $accent-color

    &__form
        display: flex
        flex-direction: column
        gap: 8px
        margin: 20px 0

    &__phone
        display: flex

        &-select
          width: 91px
          border-top-right-radius: 0
          border-bottom-right-radius: 0

        &-input
          margin-left: -1px
          border-top-left-radius: 0
          border-bottom-left-radius: 0
        

    &__check-promocode
      height: 32px

    &__btn
      margin-top: 32px
      margin-bottom: 12px

    &__link
      display: flex
      justify-content: center
</style>
