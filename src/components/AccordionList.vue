<template>
  <div class="accordion-list">
    <slot />
  </div>
</template>

<script>
  export default {
    provide() {
      return {
        accordionListState: this.sharedState
      }
    },
    data() {
      return {
        sharedState: {
          activeItem: null
        }
      };
    }
  }
</script>
