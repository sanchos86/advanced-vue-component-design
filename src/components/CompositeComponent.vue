<script>
  import ToggleInput from '@/components/ToggleInput.vue';

  export default {
    data() {
      return {
        toggled: true
      };
    },
    render(createElement) {
      return createElement(ToggleInput, {
        props: {
          checked: this.toggled
        },
        on: {
          change: newValue => this.toggled = newValue
        }
      });
    }
  }
</script>
