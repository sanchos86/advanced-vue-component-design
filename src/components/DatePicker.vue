<template>
  <label class="data-picker">
    <span class="data-picker__label">Select a date</span>
    <input type="text" ref="input" :value="date">
  </label>
</template>

<script>
  import Pikaday from 'pikaday';

  export default {
    name: 'DatePicker',
    props: {
      date: {
        type: Date,
        required: true
      },
      options: {
        type: Object,
        default: () => ({})
      }
    },
    model: {
      prop: 'date'
    },
    mounted() {
      const datepicker = new Pikaday({
        field: this.$refs.input,
        onSelect: () => {
          this.$emit('input', datepicker.getDate());
        },
        ...this.options
      });
    }
  }
</script>

<style scoped>
  @import '~pikaday/css/pikaday.css';

  .data-picker__label {
    display: block;
    margin-bottom: 8px;
  }
</style>
