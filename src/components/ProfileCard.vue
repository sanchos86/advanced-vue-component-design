<template>
  <WithDimensions>
    <template v-slot:default="{ width }">
      <div class="profile-card" :class="{ 'profile-card--horizontal': width >= 400 }">
        <img class="profile-card-image" src="../assets/logo.png" alt="">
        <div class="profile-card-meta">
          <div class="mb-4">
            <p class="text-xl leading-tight">Tony Flenderson</p>
            <p class="text-sm leading-tight text-grey-dark">Human Resources at Dynamo Moscow</p>
          </div>
          <div>
            <button class="btn btn-sm btn-pill btn-indigo-outline">Message</button>
          </div>
        </div>
      </div>
    </template>
  </WithDimensions>
</template>

<script>
  import WithDimensions from '@/components/WithDimensions.vue';

  export default {
    components: {
      WithDimensions
    }
  };
</script>
