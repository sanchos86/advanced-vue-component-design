<template>
  <span
    class="toggle-input"
    tabindex="0"
    role="checkbox"
    :class="classes"
    :aria-checked="checked.toString()"
    @click="toggle"
    @keydown.space.prevent="toggle"
  ></span>
</template>

<script>
  export default {
    name: 'ToggleInput',
    props: {
      checked: {
        type: Boolean
      }
    },
    model: {
      prop: 'checked',
      event: 'change'
    },
    computed: {
      classes() {
        return [
          { 'toggle-input--checked': this.checked }
        ];
      }
    },
    methods: {
      toggle() {
        this.$emit('change', !this.checked);
      }
    }
  };
</script>

<style scoped>
  .toggle-input {
    position: relative;
    display: inline-flex;
    width: 64px;
    height: 32px;
    border-radius: 16px;
    background-color: var(--color-secondary);
    outline: 0;
  }

  .toggle-input:focus {
    box-shadow: 0 0 0 2px rgba(0, 123, 255, .5);
  }

  .toggle-input::before {
    position: absolute;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: var(--color-primary);
    top: 50%;
    left: 1px;
    transform: translateY(-50%);
    transition: left .2s ease;
    content: "";
  }

  .toggle-input--checked::before {
    left: calc(100% - 31px);
  }
</style>
