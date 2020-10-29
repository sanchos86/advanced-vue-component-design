<script>
  export default {
    render(createElement) {
      return createElement('span', {
        attrs: {
          class: 'btn btn-small btn-success'
        }
      }, this.$slots.default);
    }
  };
</script>
