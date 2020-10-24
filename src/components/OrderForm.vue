<template>
  <div class="text-center my-4">
    <button class="btn btn-info" @click="show = true">Open modal</button>
    <Modal :show="show" @close="show = false">
      <template v-slot:submit>
        <DeleteAccountButton :account-id="accountId" />
      </template>
    </Modal>
  </div>
</template>

<script>
  import Modal from '@/components/Modal.vue';
  import DeleteAccountButton from '@/components/DeleteAccountButton.vue';

  export default {
    components: {
      Modal,
      DeleteAccountButton
    },
    data() {
      return {
        show: false,
        accountId: Math.random()
      };
    }
  };
</script>

<style scoped>

</style>
