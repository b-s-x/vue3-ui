<script setup lang="ts">
import { useSlots, useAttrs } from 'vue';
import {
  NUMBER_CHARS,
  SERVICE_CHARS,
  ALLOWED_INPUT_TYPE,
} from '../utils/input.ts';
const slots = useSlots();
const attrs = useAttrs();

interface InputEmit {
  (eventName: 'input', value: string | number): void,
  (eventName: 'keydown', value: string | number): void,
};
const emit = defineEmits<InputEmit>();

const ALLOWED_SYMBOLS: string[] = [...NUMBER_CHARS, ...SERVICE_CHARS];
const DEFAULT_INPUT_TYPE: string = 'text';

const props = defineProps({
  fullwidth: {
    type: Boolean,
    default: false,
  },
  align: {
    type: String,
    default: 'left',
    validator: align => ['left', 'center', 'right'].includes(align),
  },
  error: {
    type: Boolean,
    default: false,
  },
  errorText: {
    type: String,
    default: '',
  },
  value: {
    type: [String, Number],
    required: true,
  },
  refName: {
    type: String,
    default: '',
  },
  tooltipText: {
    type: String,
    default: '',
  },
  type: {
    type: String,
    default: 'text',
    validator: type => [
      'date',
      'email',
      'number',
      'password',
      'tel',
      'text',
      'url',
    ].includes(type),
  },
});

const mapType = (type: string): string => {
  if (!ALLOWED_INPUT_TYPE.includes(type)) return DEFAULT_INPUT_TYPE;
  if (type === 'number') return 'tel';
  return type;
};

const handleInput = (e: Event): void => emit('input', e.target.value);
const handleKeydown = (e: Event): void => emit('keydown', e.keyCode || e.which);

</script>

<template>
  <span
    :key="$data.key"
    :class="[
      'input',
      {'input_fullwidth': props.fullwidth}
    ]"
  >
    <input
      v-bind="$attrs"
      :type="mapType(props.type)"
      :readonly="$attrs.readonly"
      :ref="props.refName ? props.refName : undefined"
      :class="[
        'input_input',
        {'input_input_fullwidth': props.fullwidth},
        {'input_input_right': props.align === 'right'},
        {'input_input_center': props.align === 'center'},
        {'input_input_error': props.error},
        {'input_input_empty': !props.value},
      ]"
      @input="handleInput"
      @keydown="handleKeydown"
    />
    <span
      class="input_tooltip"
      v-if="props.tooltipText"
    >
      {{props.tooltipText}}
    </span>
    <span
      :class="['input_tooltip', 'input_tooltip_error']"
      v-if="props.errorText"
    >
      {{props.errorText}}
    </span>
  </span>
</template>

<style lang="scss">
@import "../theme/common";
$border-color_invalid: $color-red-500;
$border-color_static: $color-white-600;
$border-radius: $border-radius;
$border-radius_static: 0;
$border: 1px solid $color-gray-500;
$font-size: 1rem;
$font-size_tooltip: .75rem;
$height: 2.125rem;
$outline: unset;
$padding: 0 .625rem;
$tooltip-arrow-left: .625rem;
$tooltip-arrow-size: .375rem;
$tooltip-bg-color: $color-primary;
$tooltip-border-radius: .25rem;
$tooltip-padding: calc(.625rem / .125rem) .625rem;
$tooltip-top: 2.125rem + .5rem;


.input {
  display: inline-block;
  position: relative;
  vertical-align: middle;

  &_fullwidth {
    width: 100%;
  }

  &_input:focus ~ &_tooltip:not(&_tooltip_error) {
    opacity: 1;
    transform: translateY(0);
  }

  &_input_error:focus ~ &_tooltip_error,
  &_input:invalid:focus ~ &_tooltip_error {
    opacity: 1;
    transform: translateY(0);
  }
}

.input_input {
  border: $border;
  border-radius: $border-radius;
  box-shadow: 0 0 0 transparent;
  box-sizing: border-box;
  font: $font-size $u-font-family;;
  height: $height;
  padding: $padding;
  transition:
    border-color .2s,
    box-shadow .2s;

  &:focus {
    border-color: $color-primary;
    outline: $outline;
  }

  &:invalid:not(&_empty),
  &_error {
    border-color: $border-color_invalid;
  }

  &::placeholder {
    color: $color-gray-400;
    opacity: 1;
  }

  &_fullwidth {
    width: 100%;
  }

  &_center {
    text-align: center;
  }

  &_right {
    text-align: right;
  }

  &_static {
    border-radius: $border-radius_static;
    caret-color: transparent;

    &,
    &:focus {
      background-color: $color-white-600;
      border-color: $border-color_static;
      box-shadow: none;
    }
  }
}

.input_tooltip {
  background-color: $tooltip-bg-color;
  border-radius: $tooltip-border-radius;
  color: $color-white-500;
  display: block;
  font-size: $font-size_tooltip;;
  left: 0;
  opacity: 0;
  padding: $tooltip-padding;
  pointer-events: none;
  position: absolute;
  top: $tooltip-top;
  transform: translateY(-50%);
  transition: opacity .25s ease, transform .3s ease;
  z-index: 1;

  &::after {
    border: $tooltip-arrow-size solid transparent;
    border-bottom-color: $tooltip-bg-color;
    bottom: 100%;
    content: '';
    display: block;
    left: $tooltip-arrow-left;
    position: absolute;
  }

  &_error {
    background-color: $color-red-500;

    &::after {
      border-bottom-color: $color-red-500;
    }
  }
}

</style>
