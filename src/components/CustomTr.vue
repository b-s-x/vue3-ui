
<script lang="tsx">
import { defineComponent } from 'vue'

const props = {
  head: {
    type: Boolean,
    default: false,
  },
  filter: {
    type: Boolean,
    default: false,
  },
};

export default defineComponent({
  render({ $slots, $attrs }: any) {
    console.log(1);
    const cells = $slots.default()
      // .filter(({ type }: {type: string}): boolean => type === 'td')
      // .map((td: any) => console.log(4, td));

    // const cells = ($slots.default())
    //   .filter(child => child.tag === 'td')
    //   .map(td => {
    //     if (props.head && td.data) {
    //       td.data.staticClass = 'u-table_td_head';
    //     }

    //     return td;
    //   })
    // ;

    console.log($slots.default());


    return (
      <tr
        {...{
          ...$attrs,
          class: [
            'table_tr',
            {'table_tr_head': props.head},
            {'table_tr_filter': props.filter},
          ],
        }}
      >
        {$slots.default()}
      </tr>
    )
  }
})
</script>

