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
    <hr>
    <h3 class="mb-4">Lesson 25. Building an Element Query Component</h3>
    <div class="d-flex justify-content-center mb-8">
      <div class="w-25">
        <ProfileCard />
      </div>
    </div>
    <hr>
    <h3 class="mb-4">Lesson 26. Compound Components and ProvideInject</h3>
    <div class="max-w-sm mx-auto mb-8">
      <AccordionList>
        <AccordionItem :item-id="1">
          <template v-slot:header>
            Item 1
          </template>
          <template v-slot:content>
            <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores corporis cumque dolorum facere hic
              in, labore laudantium, magni pariatur perferendis repellat repudiandae rerum vel! Aliquid aperiam
              molestias perspiciatis sunt tempore?
            </div>
            <div>Ad alias asperiores culpa cum, delectus distinctio dolor dolores dolorum illo ipsa natus nemo nostrum
              perspiciatis quia quibusdam quidem quo ratione reiciendis sit soluta sunt temporibus voluptates! Beatae,
              dolorum soluta.
            </div>
            <div>Amet asperiores assumenda blanditiis earum exercitationem illo impedit ipsum modi molestiae nesciunt,
              obcaecati officia qui quidem quisquam similique velit voluptatem! Alias atque eum illum incidunt saepe
              sunt ullam veniam voluptates?
            </div>
          </template>
        </AccordionItem>
        <AccordionItem :item-id="2">
          <template v-slot:header>
            Item 2
          </template>
          <template v-slot:content>
            <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores corporis cumque dolorum facere hic
              in, labore laudantium, magni pariatur perferendis repellat repudiandae rerum vel! Aliquid aperiam
              molestias perspiciatis sunt tempore?
            </div>
            <div>Ad alias asperiores culpa cum, delectus distinctio dolor dolores dolorum illo ipsa natus nemo nostrum
              perspiciatis quia quibusdam quidem quo ratione reiciendis sit soluta sunt temporibus voluptates! Beatae,
              dolorum soluta.
            </div>
          </template>
        </AccordionItem>
        <AccordionItem :item-id="3">
          <template v-slot:header>
            Item 3
          </template>
          <template v-slot:content>
            <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad aperiam architecto blanditiis consequuntur
              debitis dignissimos dolor doloremque dolores facilis id, natus nobis odit omnis saepe tempore temporibus
              voluptas voluptatibus voluptatum!
            </div>
            <div>Aliquid cumque dolore quaerat quisquam! Accusantium adipisci amet asperiores aspernatur autem beatae
              consequatur culpa deleniti, ducimus error facere facilis fuga id impedit labore libero, maiores minus
              numquam odio tenetur, voluptatum.
            </div>
            <div>Architecto at atque consectetur cum expedita in incidunt ipsam iure maxime, molestias odit provident
              repellendus sapiente sint ut. Amet cupiditate dicta eveniet excepturi magnam natus similique veniam,
              voluptate? Eaque, nulla.
            </div>
            <div>Accusantium, aliquam animi asperiores blanditiis cumque cupiditate debitis dignissimos dolore eligendi
              enim exercitationem explicabo, fuga harum iure labore minima, nostrum praesentium quae quasi ratione rem
              reprehenderit saepe sint voluptates voluptatibus?
            </div>
            <div>Aperiam asperiores autem culpa delectus earum error, exercitationem expedita fugiat in inventore
              laudantium libero magni modi officiis pariatur perspiciatis quia quidem quisquam, quo quos ratione
              reprehenderit tempore temporibus vero voluptas!
            </div>
          </template>
        </AccordionItem>
      </AccordionList>
    </div>
    <hr>
    <h3 class="mb-4">Lesson 27. Building a Compound Sortable List Component</h3>
    <!--  TODO wrap in data provider  -->
    <div class="max-w-sm mx-auto mb-8">
      <div class="card">
        <h1 class="text-2xl font-bold mb-6">Contacts</h1>
        <SortableList v-model="contacts">
          <template v-slot:default="{ items: contacts }">
            <div class="contact-list">
              <SortableItem
                v-for="contact in contacts"
                :key="contact.id"
              >
                <div class="contact-list-item">
                  <div class="contact-list-contact">
                    <img class="contact-list-avatar" :src="contact.avatar" alt="">
                    <div>
                      <div class="contact-list-name">{{ contact.name }}</div>
                      <div class="contact-list-email">{{ contact.email }}</div>
                    </div>
                  </div>
                  <SortableHandle>
                    <svg
                      class="contact-list-handle"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 24 24"
                      fill="currentColor"
                    >
                      <path fill-rule="evenodd" d="M14 4h2a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1h-2a1 1 0 0 1-1-1V5a1 1 0 0 1 1-1zM8 4h2a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1H8a1 1 0 0 1-1-1V5a1 1 0 0 1 1-1zm6 6h2a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1h-2a1 1 0 0 1-1-1v-2a1 1 0 0 1 1-1zm-6 0h2a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1H8a1 1 0 0 1-1-1v-2a1 1 0 0 1 1-1zm6 6h2a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1h-2a1 1 0 0 1-1-1v-2a1 1 0 0 1 1-1zm-6 0h2a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1H8a1 1 0 0 1-1-1v-2a1 1 0 0 1 1-1z"/>
                    </svg>
                  </SortableHandle>
                </div>
              </SortableItem>
            </div>
          </template>
        </SortableList>
      </div>
    </div>
    <hr>
    <h3>Lesson 28. Building a Search Select</h3>
    <div class="max-w-sm mx-auto bg-white rounded shadow p-8 mb-8" style="margin-bottom: 200px;">
      <div class="mb-4">
        <label class="form-label mb-2">Favorite Trash Band</label>
        <SearchSelect v-model="selectedName" :options="names" :filter-function="filterFunction" />
      </div>
    </div>
    <portal-target name="modals" />
  </div>
</template>

<script>
import faker from 'faker/locale/ru';

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
import ProfileCard from '@/components/ProfileCard.vue';
import AccordionItem from '@/components/AccordionItem.vue';
import AccordionList from '@/components/AccordionList.vue';
import SortableList from '@/components/SortableList.vue';
import SortableItem from '@/components/SortableItem.vue';
import SortableHandle from '@/components/SortableHandle.vue';
import SearchSelect from '@/components/SearchSelect.vue';

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
    StackedTagInput,
    ProfileCard,
    AccordionItem,
    AccordionList,
    SortableList,
    SortableItem,
    SortableHandle,
    SearchSelect
  },
  data() {
    return {
      checked: false,
      date: new Date(),
      users: [],
      tags: ['awesome', 'cool', 'nice', 'beautiful'],
      flowers: ['camomile', 'rose'],
      contacts: Array.from({ length: 5 }).map(() => ({
        id: faker.random.number(),
        name: faker.name.findName(),
        email: faker.internet.email(),
        avatar: faker.image.avatar()
      })),
      selectedName: '',
      names: Array.from({ length: 20 }).map(() => faker.name.findName())
    };
  },
  created() {
    fetch('https://randomuser.me/api/?results=10')
      .then(response => response.json())
      .then((response) => {
        this.users = response.results;
      })
      .catch(error => console.error(error));
  },
  methods: {
    filterFunction(search, options) {
      return options.filter(el => el.endsWith(search));
    }
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
