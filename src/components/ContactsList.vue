<template>
  <div class="contacts-list my-4">
    <div v-for="(user, index) in users" :key="index" class="contacts-list__item" :class="{ 'contacts-list__item--last': users.length - 1 === index }">
      <img class="contacts-list__picture" :src="user.picture.medium" :alt="user.login.username">
      <div class="contacts-list__info">
        <h6 class="contacts-list__name">{{ `${user.name.title} ${user.name.first} ${user.name.last}` }}</h6>
        <div class="contacts-list__email">
          <slot name="email" :user="user" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      users: {
        type: Array,
        required: true
      }
    }
  };
</script>

<style scoped>
  .contacts-list {
    width: 500px;
    border-radius: 4px;
    box-shadow: 0 1px 4px 0 rgba(48, 49, 51, .5);
    padding: 16px;
  }

  .contacts-list__item {
    display: flex;
    align-items: center;
    margin-bottom: 16px;
  }

  .contacts-list__item--last {
    margin-bottom: 0;
  }

  .contacts-list__info {
    text-align: left;
  }

  .contacts-list__name {
    font-size: 1.25rem;
  }

  .contacts-list__picture {
    flex-shrink: 0;
    border-radius: 50%;
    margin-right: 16px;
  }
</style>
