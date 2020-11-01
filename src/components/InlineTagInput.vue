<template>
  <RenderlessTagInput :tags="tags" @update="(newTags) => $emit('update', newTags)">
    <template v-slot:default="{ tags, buttonEvents, inputProps, inputEvents }">
      <div class="tag-input">
        <span v-for="tag in tags" :key="tag" class="tag-input-tag">
          <span>{{ tag }}</span>
          <button type="button" class="tag-input-remove" v-on="buttonEvents(tag)">&times;</button>
        </span>
        <input type="text" class="tag-input-text" placeholder="Add tag..." v-bind="inputProps" v-on="inputEvents">
      </div>
    </template>
  </RenderlessTagInput>
</template>

<script>
  import RenderlessTagInput from '@/components/RenderlessTagInput.vue';

  export default {
    components: {
      RenderlessTagInput
    },
    model: {
      prop: 'tags',
      event: 'update'
    },
    props: {
      tags: {
        type: Array,
        default: () => ([])
      }
    }
  };
</script>
