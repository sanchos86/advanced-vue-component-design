<script>
  export default {
    props: {
      tag: {
        type: String,
        required: true
      },
      text: {
        type: String,
        default: 'Hello, world!'
      }
    },
    render(createElement) {
      return createElement(this.tag, {
        attrs: {
          class: 'btn btn-small btn-danger'
        }
      }, this.text);
    }
  }
</script>
