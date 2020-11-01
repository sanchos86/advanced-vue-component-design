<script>
  import elementResizeDetectorMaker from 'element-resize-detector';

  const erd = new elementResizeDetectorMaker({ strategy: 'scroll' });

  export default {
    data() {
      return {
        width: null,
        height: null
      };
    },
    mounted() {
      erd.listenTo(this.$el, (element) => {
        this.width = element.offsetWidth;
        this.height = element.offsetHeight
      })
    },
    render() {
      return this.$scopedSlots.default({
        width: this.width,
        height: this.height
      })
    }
  };
</script>
