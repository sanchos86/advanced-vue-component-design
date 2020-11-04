<template>
  <OnClickOutside :do="close">
    <div class="search-select" :class="{ 'is-active': isOpen }">
      <button ref="button" @click="open" type="button" class="search-select-input">
        <span v-if="value">{{ value }}</span>
        <span v-else class="search-select-placeholder">Select a band...</span>
      </button>
      <div v-show="isOpen" ref="dropdown" class="search-select-dropdown">
        <input
          v-model="search"
          ref="input"
          type="text"
          class="search-select-search"
          @keydown.esc="close"
          @keydown.up="highlightPrev"
          @keydown.down="highlightNext"
          @keydown.enter.prevent="selectHighlighted"
          @keydown.tab.prevent
        >
        <ul ref="options" v-show="filteredOptions.length > 0" class="search-select-options">
          <li
            v-for="(option, i) in filteredOptions"
            :key="option"
            class="search-select-option text-left"
            :class="{ 'is-active': i === highlightedIndex }"
            @click="select(option)"
          >
            {{ option }}
          </li>
        </ul>
        <div
          v-show="filteredOptions.length === 0"
          class="search-select-empty text-left"
        >
          No results found for %{{ search }}%
        </div>
      </div>
    </div>
  </OnClickOutside>
</template>

<script>
  import { createPopper } from '@popperjs/core';
  import OnClickOutside from '@/components/OnClickOutside.vue';

  export default {
    components: {
      OnClickOutside
    },
    props: {
      value: {
        type: String
      },
      options: {
        type: Array,
        required: true
      },
      filterFunction: {
        type: Function,
        default: (search, options) => {
          return options.filter(el => el.toLowerCase().startsWith(search.toLowerCase()));
        }
      }
    },
    data() {
      return {
        isOpen: false,
        search: '',
        highlightedIndex: 0
      };
    },
    computed: {
      filteredOptions() {
        return this.filterFunction(this.search, this.options);
      }
    },
    beforeDestroy() {
      this.popper.destroy();
    },
    methods: {
      setupPopper() {
        if (this.popper === undefined) {
          this.popper = createPopper(this.$refs.button, this.$refs.dropdown, {
            placement: 'bottom',
            modifiers: [
              {
                name: 'offset',
                options: {
                  offset: [0, 5],
                },
              },
            ]
          })
        }
      },
      open() {
        if (this.isOpen) {
          return;
        }
        this.isOpen = true;
        this.$nextTick(() => {
          this.setupPopper();
          this.$refs.input.focus();
          this.scrollToHighlighted();
        });
      },
      close() {
        if (!this.isOpen) {
          return;
        }
        this.isOpen = false;
        this.$refs.button.focus();
      },
      select(option) {
        this.$emit('input', option);
        this.search = '';
        this.highlightedIndex = 0;
        this.close();
      },
      scrollToHighlighted() {
        this.$refs.options.children[this.highlightedIndex].scrollIntoView({
          block: "nearest"
        });
      },
      selectHighlighted() {
        this.select(this.filteredOptions[this.highlightedIndex]);
      },
      highlight(index) {
        this.highlightedIndex = index;
        if (this.highlightedIndex > this.filteredOptions.length - 1) {
          this.highlightedIndex = 0;
        }
        if (this.highlightedIndex < 0) {
          this.highlightedIndex = this.filteredOptions.length - 1;
        }
        this.scrollToHighlighted();
      },
      highlightNext() {
        this.highlight(this.highlightedIndex + 1);
      },
      highlightPrev() {
        this.highlight(this.highlightedIndex - 1);
      }
    }
  }
</script>
