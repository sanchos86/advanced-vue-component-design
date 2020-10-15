<template>
  <div class="announcement-modal">
    <button @click="show = true">Show modal</button>
    <Modal :show="show" @close="show = false" />
  </div>
</template>

<script>
  import Modal from '@/components/Modal';

  export default {
    name: "AnnouncementModal",
    components: {
      Modal
    },
    data() {
      return {
        show: false
      };
    }
  }
</script>

<style scoped>

</style>
