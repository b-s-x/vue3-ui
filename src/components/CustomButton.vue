<script lang="tsx" setup >
const props = defineProps({
  appearance: {
    type: String,
    default: 'solid',
    validator: appearance =>
      ['solid', 'outline', 'control'].includes(appearance),
  },
  color: {
    type: String,
    default: 'primary',
    validator: color => ['primary', 'secondary', 'danger'].includes(color),
  },
  size: {
    type: String,
    default: 'medium',
    validator: size => ['small', 'square', 'medium', 'wide'].includes(size),
  },
});
</script>

<script lang="tsx">
import { defineComponent, h } from 'vue'

export default defineComponent({
  render({ props, $slots, $attrs }) {
    return h(
      'button',
      {
        ...$attrs,
        class: [
          'button',
          `button_${props.appearance}`,
          `button_${props.color}`,
          `button_${props.size}`,
        ]
      },
      [
        $slots.default(),
      ],
    );
  }
})
</script>

<style lang="scss">
@import "../theme/common";

$bg-control: transparent;
$bg-control_active: darken(desaturate($color-white-600, 6.7), 4.3);
$bg-control_disabled: transparent;
$bg-control_hover: $color-white-600;
$bg-danger: $color-red-400;
$bg-danger_active: $color-red-300;
$bg-danger_disabled: $color-red-200;
$bg-danger_hover: $color-red-500;
$bg-primary: $color-black-500;
$bg-primary_active: $color-black-500;
$bg-primary_disabled: $color-gray-700;
$bg-primary_hover: $color-gray-900;
$bg-secondary: $color-gray-600;
$bg-secondary_active: $color-gray-500;
$bg-secondary_disabled: $color-gray-300;
$bg-secondary_hover: $color-gray-600;

$border-radius: $border-radius;
$border-width: 1px;
$box-sizing: border-box;

$color-control: $color-gray-900;
$color-danger: $color-red-500;
$color-primary: $color-red-500;
$color-secondary: $color-gray-600;
$color-white: $color-white-500;

$font-size: 1rem;
$height-control: auto;
$height: 1rem;
$min-width-control: 0;
$min-width: 64px;
$min-width_small: 0;
$padding-control: 1rem / 2 1rem;
$padding: 1rem;
$padding_small: 0;
$padding_wide: 0 (4 * 1rem);
$text-transform: lowercase;
$transition: color .2s,
  background-color .2s,
  border-color .2s;
$unset-focus-outline: true;
$use-disabled-cursor: true;

.button {
  align-items: center;
  border: $border-width solid transparent;
  border-radius: $border-radius;
  box-sizing: $box-sizing;
  display: inline-flex;
  font: $font-size $font-family;
  height: $height;
  justify-content: center;
  text-transform: $text-transform;
  transition: $transition;
  vertical-align: middle;

  @if ($unset-focus-outline) {
    &:focus {
      outline: none;
    }
  }

  @if ($use-disabled-cursor) {
    &:disabled {
      cursor: not-allowed;
    }
  }

  // sizes
  &_small {
    min-width: $min-width_small;
    padding: $padding;
  }

  &_square {
    min-width: $height;
    padding: 0;
  }

  &_medium {
    min-width: $min-width;
    padding: $padding;
  }

  &_wide {
    min-width: $min-width;
    padding: $padding_wide;
  }

  // colors
  &_primary {
    @include button-color(
      $color-primary,
      $bg-primary,
      $bg-primary_active,
      $bg-primary_disabled,
      $bg-primary_hover,
    );
  }

  &_secondary {
    @include button-color(
      $color-secondary,
      $bg-secondary,
      $bg-secondary_active,
      $bg-secondary_disabled,
      $bg-secondary_hover,
    );
  }

  &_danger {
    @include button-color(
      $color-danger,
      $bg-danger,
      $bg-danger_active,
      $bg-danger_disabled,
      $bg-danger_hover,
    );
  }

  // appearance
  &_solid {
    &,
    &:disabled {
      color: $color-white;
    }
  }

  &_outline {
    background-color: transparent;

    &:disabled {
      background-color: transparent;
    }

    &:hover:not(:disabled),
    &:focus:not(:disabled) {
      color: $color-white;
    }
  }

  &_control {
    height: $height-control;
    min-width: $min-width-control;
    padding: $padding-control;

    @include button-color(
      $color-control,
      $bg-control,
      $bg-control_active,
      $bg-control_disabled,
      $bg-control_hover
    );

    &:disabled {
      color: $color-gray-600;
    }
  }
}

</style>
