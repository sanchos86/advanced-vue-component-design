<script>
  export default {
    model: {
      prop: 'tags',
      event: 'update'
    },
    props: {
      tags: {
        type: Array,
        default: () => ([])
      },
      removeOnBackSpace: {
        type: Boolean,
        default: true
      }
    },
    data() {
      return {
        input: ''
      };
    },
    computed: {
      newTag() {
        return this.input.trim();
      }
    },
    methods: {
      clearInput() {
        this.input = '';
      },
      addTag() {
        if (this.newTag.length === 0 || this.tags.includes(this.newTag)) {
          return;
        }
        this.$emit('update', [...this.tags, this.newTag]);
        this.clearInput();
      },
      removeTag(tag) {
        this.$emit('update', this.tags.filter(el => el !== tag));
      },
      handleBackSpace() {
        if (this.newTag.length === 0) {
          this.$emit('update', this.tags.slice(0, -1));
        }
      }
    },
    render() {
      return this.$scopedSlots.default({
        tags: this.tags,
        addTag: this.addTag,
        buttonEvents: (tag) => ({
          click: () => this.removeTag(tag)
        }),
        inputEvents: {
          input: (e) => { this.input = e.target.value },
          keydown: (e) => {
            if (e.key === 'Backspace' && this.removeOnBackSpace) {
              this.handleBackSpace();
            }
            if (e.key === 'Enter') {
              e.preventDefault();
              this.addTag();
            }
          }
        },
        inputProps: {
          value: this.input
        }
      })
    }
  }
</script>
