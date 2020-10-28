<script>
  import faker from 'faker';

  export default {
    data() {
      return {
        contacts: Array.from({ length: 5 }).map(() => ({
          name: faker.name.findName(),
          uuid: faker.random.uuid()
        }))
      };
    },
    render(createElement) {
      const heading = 'Lesson 14. Render Functions And Children';
      return createElement('div', {
        attrs: {
          class: 'mb-4'
        }
      }, [
        createElement('h3', {}, heading),
        createElement('ul', {
          style: {
            listStyleType: 'none'
          }
        }, this.contacts.map(el => createElement('li', {
          class: {
            'font-italic': true
          }
        }, `${el.uuid}: ${el.name}`)))
      ])
    }
  };
</script>
