<script>
  import { Sortable } from '@shopify/draggable';

  function move(items, oldIndex, newIndex) {
    const itemRemovedArray = [
      ...items.slice(0, oldIndex),
      ...items.slice(oldIndex + 1, items.length)
    ]

    return [
      ...itemRemovedArray.slice(0, newIndex),
      items[oldIndex],
      ...itemRemovedArray.slice(newIndex, itemRemovedArray.length)
    ]
  }

  export default {
    props: {
      itemClass: {
        type: String,
        default: 'sortable-item'
      },
      handleClass: {
        type: String,
        default: 'sortable-handle'
      },
      value: {
        type: Array,
        required: true
      }
    },
    provide() {
      return {
        sortableItemClass: this.itemClass,
        sortableHandleClass: this.handleClass
      };
    },
    render() {
      return this.$scopedSlots.default({
        items: this.value
      });
    },
    mounted() {
      new Sortable(this.$el, {
        draggable: `.${this.itemClass}`,
        handle: `.${this.handleClass}`,
        mirror: {
          constrainDimensions: true
        }
      })
        .on('sortable:stop', ({ oldIndex, newIndex }) => {
        this.$emit("input", move(this.value, oldIndex, newIndex))
      })
    }
  }
</script>
