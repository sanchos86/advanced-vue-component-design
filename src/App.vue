<template>
  <div id="app">
    <ToggleInput v-model="checked" />
    <hr>
    <DatePicker v-model="date" :options="{ firstDay: 1 }" />
    <hr>
    <AnnouncementModal />
    <hr>
    <OrderForm />
    <hr>
    <div class="d-flex justify-content-center">
      <MediaCard class="mb-4" />
    </div>
    <div class="d-flex justify-content-center">
      <MediaCard class="mb-4">
        <template v-slot:header>Media card</template>
        <p class="card-text">
          <span>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Adipisci architecto culpa eveniet excepturi facilis harum illo iusto libero maxime molestias odio quam quibusdam, quis quo repellat reprehenderit suscipit vero vitae!</span><span>Adipisci alias aperiam beatae consequatur culpa dolor dolores eius ex exercitationem expedita harum, impedit in modi molestias necessitatibus non officia porro quam quidem recusandae repudiandae saepe sequi temporibus, totam veritatis.</span><span>Deserunt fugit maiores nihil nobis odio optio porro praesentium quisquam repellendus vitae? Aut autem delectus ea minima natus non nostrum nulla omnis optio quo, repellat velit. Distinctio odit quis reiciendis!</span>
        </p>
      </MediaCard>
    </div>
    <hr>
    <div class="d-flex justify-content-center">
      <ContactsList :users="users">
        <template v-slot:email="{ user }">
          <a :href="`mailto:${user.email}`">{{ user.email }}</a>
        </template>
      </ContactsList>
    </div>
    <hr>
    <div class="mb-4">
      <h3>Lesson 12. Render Functions 101</h3>
      <HelloWorld tag="button" text="Обычным языком средневекового европейского письма был латинский." />
    </div>
    <hr>
    <div class="mb-4">
      <h3>Lesson 13. Render Functions And Components</h3>
      <CompositeComponent />
    </div>
    <BigComponent />
    <hr>
    <h3>Lesson 15. Render Functions And Slots</h3>
    <div class="text-center mb-4">
      <RenderAndSlots>
        <template v-slot:default="{ name }">
          <strong>{{ name }}</strong>
        </template>
      </RenderAndSlots>
    </div>
    <div class="text-center mb-4">
      <RenderAndSlotsV2>RenderAndSlotsV2</RenderAndSlotsV2>
    </div>
    <portal-target name="modals" />
  </div>
</template>

<script>
import ToggleInput from './components/ToggleInput.vue'
import DatePicker from '@/components/DatePicker';
import AnnouncementModal from '@/components/AnnouncementModal.vue';
import OrderForm from '@/components/OrderForm.vue';
import MediaCard from '@/components/MediaCard.vue';
import ContactsList from '@/components/ContactsList.vue';
import HelloWorld from '@/components/HelloWorld.vue';
import CompositeComponent from '@/components/CompositeComponent.vue';
import BigComponent from '@/components/BigComponent.vue';
import RenderAndSlots from '@/components/RenderAndSlots.vue'
import RenderAndSlotsV2 from '@/components/RenderAndSlotsV2.vue'

export default {
  name: 'App',
  components: {
    DatePicker,
    ToggleInput,
    AnnouncementModal,
    OrderForm,
    MediaCard,
    ContactsList,
    HelloWorld,
    CompositeComponent,
    BigComponent,
    RenderAndSlots,
    RenderAndSlotsV2
  },
  data() {
    return {
      checked: false,
      date: new Date(),
      users: []
    };
  },
  created() {
    fetch('https://randomuser.me/api/?results=10')
      .then(response => response.json())
      .then((response) => {
        this.users = response.results;
      })
      .catch(error => console.error(error));
  }
}
</script>

<style>
:root {
  --color-primary: #007bff;
  --color-secondary: #dae0e5;
  --color-grey: #cccccc;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
