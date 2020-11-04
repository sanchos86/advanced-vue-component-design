<script>
  export default {
    props: {
      do: {
        type: Function,
        default: () => {}
      }
    },
    mounted() {
      const handler = (e) => {
        if (this.$el === e.target || this.$el.contains(e.target)) {
          return;
        }
        this.do();
      };
      document.addEventListener('click', handler);
      this.$once('hook:beforeDestroy', () => {
        document.removeEventListener('click', handler);
      })
    },
    render() {
      return this.$slots.default[0];
    }
  };
</script>
