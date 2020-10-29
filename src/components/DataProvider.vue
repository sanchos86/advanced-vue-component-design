<script>
  export default {
    props: {
      url: {
        type: String,
        required: true
      }
    },
    data() {
      return {
        loading: true,
        data: null
      }
    },
    async created() {
      const response = await fetch(this.url);
      const { results } = await response.json();
      setTimeout(() => {
        this.data = results;
        this.loading = false;
      }, 1500);
    },
    render() {
      return this.$scopedSlots.default({
        loading: this.loading,
        data: this.data
      })
    }
  }
</script>
