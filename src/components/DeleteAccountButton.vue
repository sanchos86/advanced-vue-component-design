<template>
  <button @click="show = true">
    <slot />
    <portal to="modals">
      <Modal :show="show" @close="show = false">
        <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam asperiores aspernatur doloremque ex,
          ipsam magni quod ratione sit ullam vel? Blanditiis dignissimos fugit iure libero molestiae molestias mollitia,
          necessitatibus quos?
        </div>
        <div>Exercitationem iusto quibusdam ratione tempore voluptas. Ad asperiores autem deleniti dicta dolores
          doloribus eligendi eos et eum exercitationem, expedita facilis iste laborum maxime, minus nostrum odio odit
          perferendis quisquam voluptate.
        </div>
        <div>Aspernatur, atque blanditiis commodi consectetur cupiditate deleniti deserunt distinctio doloremque dolorum
          eaque, eius exercitationem fugiat id ipsum laboriosam minima minus nemo nesciunt officiis, optio pariatur
          perspiciatis quibusdam quis vero vitae.
        </div>
        <template v-slot:submit>
          <button class="btn btn-small btn-success" @click="deleteAccount">Yes</button>
        </template>
      </Modal>
    </portal>
  </button>
</template>

<script>
  import Modal from '@/components/Modal.vue';

  export default {
    components: {
      Modal
    },
    props: {
      accountId: {
        type: Number,
        required: true
      }
    },
    data() {
      return {
        show: false
      };
    },
    methods: {
      deleteAccount() {
        console.log(this.accountId);
      }
    }
  };
</script>

<style scoped>

</style>
