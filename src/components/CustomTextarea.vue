<script setup lang="ts">
interface TextareaEmit {
  (eventName: 'input', value: string | number): void,
};
const emit = defineEmits<TextareaEmit>();

const props = defineProps({
  error: {
    type: Boolean,
    default: false,
  },
});

const handleInput = (e: Event): void => emit('input', e.target.value);

</script>

<template>
  <div class="textarea">
    <textarea
      v-bind="$attrs"
      :class="[
        'textarea_input',
        {'textarea_input_error': props.error},
        {'textarea_input_empty': !props.value},
      ]"
      @input="handleInput"
    >
      {{props.value}}
    </textarea>
  </div>

</template>

<style lang="scss">
@import "../theme/common";
$border-color: $color-gray-500;
$border-color_focus: $color-primary;
$border-color_invalid: $color-red-500;
$border-radius: $border-radius;
$border: 1px solid $border-color;
$box-shadow: 0 0 0 transparent;
$box-shadow_focus: 0 0 2px rgba($color-primary, .3);
$font-size: 1rem;
$height: 5 * 2rem;
$padding: 1rem;
$placeholder-color: $color-gray-600;

.textarea {
  display: flex;
  position: relative;
  width: 100%;
  outline: none;
  overflow: auto;

  &_input {
    box-shadow: -5px -1px 21px 0px rgba(34, 60, 80, 0.2);
    // background: $color-gray-300;
    border-radius: $border-radius;
    box-sizing: border-box;
    font: $font-size $font-family;
    max-width: 100%;
    min-height: $height;
    padding: $padding;
    transition:
      border-color .2s,
      box-shadow .2s;
    width: 100%;
    resize: none;

    &:focus {
      // box-shadow: $box-shadow_focus;
      box-shadow: -5px -1px 62px 6px rgba(34, 60, 80, 0.41);
      outline: none;
    }

    &:invalid:not(&_empty),
    &_error {
      border-color: $border-color_invalid;
    }

    &::placeholder {
      color: $placeholder-color;
      opacity: 1;
    }
  }
  &:focus {
      // box-shadow: $box-shadow_focus;
      box-shadow: -5px -1px 62px 6px rgba(34, 60, 80, 0.41);
      outline: none;
    }
}

</style>
