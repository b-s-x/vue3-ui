<script lang="tsx" setup >
const props = defineProps({
  level: {
    type: [Number, String],
    default: 1,
  },
});
</script>

<script lang="tsx">
import { defineComponent, h } from 'vue'

export default defineComponent({
  render({ props, $slots, $attrs }) {
    return h(
      `h${props.level}`,
      {
        ...$attrs,
        class: [
          'title',
          `title_h${props.level}`
        ]
      },
      [
        $slots.default(),
        $slots.sub
          ? h('div', { class: 'title_sub' }, $slots.sub())
          : null
      ],
    );
  }
})
</script>

<style lang="scss">
@import "../theme/common";
$border_h1: 1px solid $color-white-500;
$color: $color-black-500;
$color_h1: $color-gray-700;
$font-family: 'NeoSansCyr', Arial, Helvetica, sans-serif;
$font-size-base: 2rem;
$font-size-scale: .5rem;
$font-style: normal;
$font-weight: normal;
$margin: 1.5rem 0 .8rem;
$padding: 0;
$sub-font-size: 1rem;
$text-transform: lowercase;

.title {
  color: $color;
  font-family: $font-family;
  font-weight: $font-weight;
  margin: $margin;
  padding: $padding;
  text-transform: $text-transform;

  &_sub {
    color: inherit;
    font-size: $font-size-base - ($font-size-scale * 1.5);
  }

  &_h1 {
    color: $color_h1;
    font-size: $font-size-base;
  }

  &_h2 {
    font-size: $font-size-base + $font-size-scale;
  }

  &_h3 {
    font-size: $font-size-base + ($font-size-scale * 2);
  }

  &_h4 {
    font-size: $font-size-base + ($font-size-scale * 3);
  }

  &_h5 {
    font-size: $font-size-base + ($font-size-scale * 4);
  }

  &_h6 {
    font-size: $font-size-base + ($font-size-scale * 5);
  }

  &_h7 {
    font-size: $font-size-base + ($font-size-scale * 6);
  }
}

</style>
