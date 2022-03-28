<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">
      <div>
        <BaseInput v-model="event.title" label="Title" />
        <BaseInput v-model="event.description" label="Description" />
      </div>
      <div>
        <BaseSelect
          :options="categories"
          v-model="event.category"
          label="Select a category"
        />
      </div>
      <div>
        <BaseRadioGroup
          v-model="event.pets"
          name="pets"
          :options="petOptions"
          vertical
        />
      </div>
      <div>
        <BaseCheckbox v-model="event.extras.catering" label="Catering" />
        <BaseCheckbox v-model="event.extras.music" label="Live music" />
      </div>

      <button type="submit">Submit</button>
    </form>

    <pre>{{ event }}</pre>
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from 'axios';
import BaseInput from '../components/BaseInput.vue';
import BaseSelect from '../components/BaseSelect.vue';
import BaseCheckbox from '../components/BaseCheckbox.vue';
import BaseRadioGroup from '../components/BaseRadioGroup.vue';

export default {
  components: { BaseInput, BaseSelect, BaseCheckbox, BaseRadioGroup },

  setup() {
    const event = ref({
      category: '',
      title: '',
      description: '',
      pets: 1,
      extras: {
        catering: false,
        music: false,
      },
    });

    const categories = ref(['a', 'b', 'c']);

    const petOptions = ref([
      { label: 'Yes', value: 1 },
      { label: 'No', value: 0 },
    ]);

    function sendForm() {
      axios
        .post(
          'https://my-json-server.typicode.com/magazin2620/basic-form/events',
          this.event
        )
        .then(function (response) {
          console.log('Response', response);
        })
        .catch(function (err) {
          console.log('Error', err);
        });
    }

    return { event, categories, petOptions, sendForm };
  },
};
</script>
