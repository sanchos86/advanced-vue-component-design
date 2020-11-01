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
    <hr>
    <h3>Lesson 16. Data Provider Components</h3>
    <DataProvider url="https://randomuser.me/api/?results=5">
      <template v-slot:default="{ data, loading }">
        <div class="contacts-list mb-4">
          <h4>Contacts List</h4>
          <div v-if="loading">Loading...</div>
          <div v-else>
            <div v-for="item in data" :key="item.id.value">
              <div><strong>{{ item.login.username }}</strong></div>
              <div><i>{{ item.email }}</i></div>
            </div>
          </div>
        </div>
      </template>
    </DataProvider>
    <DataProvider url="https://swapi.dev/api/people">
      <template v-slot:default="{ data, loading }">
        <div class="contacts-list m-4 p-4 w-25 bg-info rounded">
          <h4>Star wars</h4>
          <div v-if="loading">Loading...</div>
          <div v-else>
            <div v-for="(item, index) in data" class="text-left mb-2" :key="index">
              <div><a :href="item.url" class="text-white" target="_blank">{{ item.name }}</a></div>
              <div><a :href="item.homeworld" class="text-white" target="_blank">Planet</a></div>
            </div>
          </div>
        </div>
      </template>
    </DataProvider>
    <hr>
    <h3 class="mb-4">Lesson 17. Getting Started With Renderless Components</h3>
    <div class="max-w-sm mx-auto card mb-8 text-left">
      <label class="form-label mb-2">Inline Tag Input</label>
      <InlineTagInput v-model="tags" />
    </div>
    <div class="max-w-sm mx-auto card mb-8 text-left">
      <label class="form-label mb-2">Stacked Tag Input</label>
      <StackedTagInput v-model="flowers" />
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
import RenderAndSlots from '@/components/RenderAndSlots.vue';
import RenderAndSlotsV2 from '@/components/RenderAndSlotsV2.vue';
import DataProvider from '@/components/DataProvider.vue';
import InlineTagInput from '@/components/InlineTagInput.vue';
import StackedTagInput from '@/components/StackedTagInput.vue';

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
    RenderAndSlotsV2,
    DataProvider,
    InlineTagInput,
    StackedTagInput
  },
  data() {
    return {
      checked: false,
      date: new Date(),
      users: [],
      tags: ['awesome', 'cool', 'nice', 'beautiful'],
      flowers: ['camomile', 'rose']
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

<style src="./assets/app.css"></style>
