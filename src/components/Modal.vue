<template>
  <div class="modal-overlay" v-show="show">
    <div class="modal">
      <div class="modal__body">
        <p class="modal__text">Советское искусствоведение воспринимало полотно Владимира Серова как одно из наиболее значительных произведений искусства, созданных в послевоенный период. Анализ замысла картины, её композиционного и колористического решения проводили в своих работах такие видные деятели советской художественной культуры, как доктор культурологии Иван Астахов, доктор искусствоведения Софья Коровкевич, доктор искусствоведения и действительный член Академии художеств СССР Андрей Лебедев.</p>
      </div>
      <div class="modal__footer">
        <button @click="dismiss">Cancel</button>
        <button>Submit</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Modal',
    props: {
      show: {
        type: Boolean,
        required: true
      },
      preventBackgroundScrolling: {
        type: Boolean,
        default: true
      }
    },
    created() {
      const closeModal = (e) => {
        if (e.key === 'Escape' && this.show) {
          this.dismiss();
        }
      };
      document.addEventListener('keydown', closeModal);
      this.$once('hook:destroyed', closeModal);
    },
    watch: {
      show: {
        handler(newValue) {
          if (newValue) {
            this.preventBackgroundScrolling && document.body.style.setProperty('overflow', 'hidden');
          } else {
            this.preventBackgroundScrolling && document.body.style.removeProperty('overflow');
          }
        },
        immediate: true
      }
    },
    methods: {
      dismiss() {
        this.$emit('close');
      }
    }
  };
</script>

<style scoped>
  .modal-overlay {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, .75);
  }

  .modal {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
    border-radius: 8px;
    max-width: 600px;
    padding: 32px;
  }

  .modal button:first-of-type {
    margin-right: 16px;
  }
</style>
