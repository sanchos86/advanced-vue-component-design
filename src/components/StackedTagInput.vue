<template>
  <RenderlessTagInput :tags="flowers" :remove-on-back-space="false" @update="(newFlowers) => $emit('update', newFlowers)">
    <template v-slot:default="{ tags: flowers, buttonEvents, inputProps, inputEvents, addTag }">
      <div class="stacked-tag-input">
        <div class="stacked-tag-input-form">
          <input type="text" class="form-input" placeholder="Add tag..." v-bind="inputProps" v-on="inputEvents">
          <button class="btn btn-indigo" @click="addTag">Add Tag</button>
        </div>
        <ul class="stacked-tag-list">
          <li v-for="flower in flowers" :key="flower">
            {{ flower }}
            <button type="button" class="stacked-tag-link" v-on="buttonEvents(flower)">Remove</button>
          </li>
        </ul>
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
      prop: 'flowers',
      event: 'update'
    },
    props: {
      flowers: {
        type: Array,
        default: () => ([])
      }
    }
  }
</script>
