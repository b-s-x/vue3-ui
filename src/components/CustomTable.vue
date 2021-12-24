<script lang="tsx" setup>

interface TableEmit {
  (eventName: 'filter', value: Event): void,
};

const emit = defineEmits<TableEmit>();
const props = defineProps({
  bottomBordered: {
    type: Boolean,
    default: false,
  },
  containerTag: {
    type: String,
    default: 'form',
  },
});
</script>

<script lang="tsx">
import { defineComponent } from 'vue'

export default defineComponent({
  render({ props, $slots, $attrs }: any) {
    const ContainerTag: any = props.containerTag || 'div';
    const rows = $slots.default().filter(({ type }: {type: string}): boolean => type === 'tr');
    const handleFilter = (e: Event): void => {
      if (props.containerTag === 'form') {
        e.preventDefault();
        emit('filter', e)
      }

      return;
    };

    return (
      <ContainerTag
        class="table"
        onSubmit={handleFilter}
      >
        <table
          {...{
            ...$attrs,
            class: [
              'table_table',
              {'table_table_bottom-bordered': props.bottomBordered}
            ],
          }}
        >
          <tbody>
            {rows}
          </tbody>
        </table>
      </ContainerTag>
    )
  }
})
</script>

<style lang="scss">
@import "../theme/common";

$base-indent: 1rem;
$table-border-bottom: 1px solid $color-gray-500;
$table-container-margin: 0 (-$base-indent);
$table-filter-indent: $base-indent;
$table-font-size: 1rem;
$table-font-size_head: 1rem;
$table-font-weight_head: bold;
$table-row-bg-color: $color-white-500;
$table-row-bg-color_even: $color-white-600;
$table-row-bg-color_head: $color-gray-400;
$table-row-color_head: $color-white-500;
$table-td-padding: $base-indent 2 * $base-indent $base-indent $base-indent;
$table-td-padding_filter: .5 * $base-indent $table-filter-indent .5 * $base-indent 0;
$table-td-padding_filter_last: .5 * $base-indent 0 .5 * $base-indent 0;
$table-td-padding_head: 1.5 * $base-indent 2 * $base-indent 1.5 * $base-indent $base-indent;
$table-td-padding_head_last: 1.5 * $base-indent $base-indent;
$table-td-padding_last: $base-indent;

.table {
  margin: $table-container-margin;

  &_table {
    border-collapse: collapse;
    border-spacing: 0;
    width: 100%;

    &_bottom-bordered {
      border-bottom: $table-border-bottom;
    }
  }

  &_td {
    background-color: $color-white-500;
    font-size: $table-font-size;
    padding: $table-td-padding_last;
    text-align: left;

    &:not(:last-child) {
      padding: $table-td-padding;
    }

    &_head {
      background-color: $table-row-bg-color_head;
      color: $table-row-color_head;
      font-size: $table-font-size_head;
      font-weight: $table-font-weight_head;
      padding: $table-td-padding_head_last;

      &:not(:last-child) {
        padding: $table-td-padding_head;
      }
    }

    &_filter {
      padding: $table-td-padding_filter_last;

      &:not(:last-child) {
        padding: $table-td-padding_filter;
      }
    }

    &_align-center {
      text-align: center;
    }

    &_align-right {
      text-align: right;
    }
  }

  &_td-filter {
    display: flex;
    justify-content: space-between;

    & > *:not(:last-child) {
      margin-right: $table-filter-indent;
    }

    & > .input {
      flex-grow: 1;

      & > .input_input {
        min-width: 0;
        width: 100%;
      }
    }

    & > .select {
      flex-grow: 1;

      & > .select_select {
        min-width: 0;
        width: 100%;
      }
    }
  }

  &_tr:not(&_tr_head):nth-of-type(even) > &_td {
    background-color: $table-row-bg-color_even;
  }

  &_tr_head ~ &_tr:nth-of-type(odd) > &_td {
    background-color: $table-row-bg-color_even;
  }

  &_tr_head ~ &_tr:nth-of-type(even) > &_td {
    background-color: $table-row-bg-color;
  }

  &_tr_filter ~ &_tr:not(&_tr_head):nth-of-type(odd) > &_td {
    background-color: $table-row-bg-color;
  }

  &_tr_filter ~ &_tr:not(&_tr_head):nth-of-type(even) > &_td {
    background-color: $table-row-bg-color_even;
  }
}

</style>
