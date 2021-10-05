<template>
  <div class="wrapper">
    <Select
      :options='options'
      v-model:opt='selectedOptions'
    />
    {{selectedOptions}}
  </div>
</template>

<script>
import Select from './components/Select.vue'

export default {
  components: {
    Select
  },
  data() {
    return {
      selectedOptions: {},
      options: [
        {
          name: 'Option 1',
          value: 1
        },
        {
          name: 'Option 2',
          value: 2
        },
        {
          name: 'Option 3',
          value: 3
        },
        {
          name: 'Option 4',
          value: 4
        },
        {
          name: 'Option 5',
          value: 5
        },
      ]
    }
  },
}
</script>

<style>

</style>
