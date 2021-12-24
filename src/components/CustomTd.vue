
<script lang="tsx">
import { defineComponent } from 'vue'

const props = {
  filter: {
    type: Boolean,
    default: false,
  },
  align: {
    type: String,
    default: 'left',
    validator: (align: string): boolean => ['left', 'center', 'right'].includes(align),
  },
};

export default defineComponent({
  render({ $slots, $attrs }: any) {
    const content = props?.filter
      ? <div class="table_td-filter">{$slots.default()}</div>
      : $slots.default()

    return (
      <td
        {...{
          ...$attrs,
          class: [
            'table_td',
            [`table_td_align-${props.align}`],
            {'table_td_filter': props?.filter},
          ],
        }}
      >
        {content}
      </td>
    )
  }
})
</script>

