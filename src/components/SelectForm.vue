<template>
  <div class="select-form" @click="isVisiable = !isVisiable">
    <div class="select-form__main">
      <div class="select-form__header">
        <div 
            class="select-form__title"
            v-if="title">
                {{ title }}
        </div>
        <div :class="placeholder === selected ? 'select-form__placeholder' : ''">
            {{ selected }}
        </div>
      </div>
      <div class="select-form__arrow">
        <img
          :class="
            isVisiable ? 'select-form__arrow__bottom' : 'select-form__arrow'
          "
          src="../assets/img/Arrow.svg"
          alt="open"
        />
      </div>
    </div>

    <div class="options-form" v-if="isVisiable">
        <img class="options-form__triangle" src="../assets/img/Triangle.svg">
      <div 
        class="options-form__option" 
        v-for="option in options" 
        :key="option"
        @click="selected = option">
        <span :class=" (option === selected) ? 'options-form__option__selected' : ''">
          {{ option }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isVisiable: false,
      selected: this.placeholder || this.options[0]
    };
  },

  props: {
    options: {
      type: Array,
    },
    placeholder: {
      type: String,
      default: "",
    },
    title: {
        type: String
    }
  },
};
</script>

<style lang="sass">
$border-color: #DCDFE6
$accent-color: #17505B

.ui 
    background-color: red


.select-form
    width: 100%
    position: relative
    flex-direction: column


    &__main
        box-sizing: border-box
        display: flex
        width: 100%
        flex-direction: row
        align-items: center
        justify-content: space-between
        padding: 10px 15px

    &__header
        display: flex
        flex-direction: column
    &__title
        margin-top: -5px 
        margin-bottom: 2px
        font-size: 8px
        color: #C0C4CC

    &__placeholder 
        color: #A8ABB2
    &__arrow
        transform: rotate(90deg)

    &__arrow__bottom
        transform: rotate(-90deg)
    





.options-form
    width: 100%
    display: flex
    flex-direction: column
    border: 1px solid $border-color
    background-color: white
    margin-top: 8px
    margin-left: -1px 
    z-index: 5

    &__triangle
        padding-left: 5%
        transform: translatey(-100%)
        width: 30px

    &__option
        display: flex
        align-items: center
        justify-content: left
        height: 34px
        color: #606266
        padding: 0px 15px

    &__option:hover 
        background-color: #F5F7FA

    &__option:active, &__option__selected
        color: $accent-color
        font-weight: 500
</style>
