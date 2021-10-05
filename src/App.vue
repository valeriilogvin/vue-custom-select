<template>
  <h2>Custom select</h2>
  <div class="wrapper">
    
    <div>
      <h3>single</h3>
      <Select
        :options='options'
        v-model="selectedSingleOptions"
      />
      <pre>{{selectedSingleOptions}}</pre>
    </div>

    <div>
      <h3>multiple</h3>
      <Select
        :options='options'
        :isMultiple="true"
        v-model="selectedMultipleOptions"
      />
      <pre>{{selectedMultipleOptions}}</pre>
    </div>

    <div>
      <h3>search</h3>
      <Select
        :options='options'
        :isSearchable="true"
        v-model="selectedSearchOptions"
      />
      <pre>{{selectedSearchOptions}}</pre>
    </div>
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
      selectedSingleOptions: {},
      selectedSearchOptions: {},
      selectedMultipleOptions: [],
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
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    background: #040402;
    font-family: 'Montserrat', sans-serif;
    color: #fff;
  }
  .wrapper{
    display: flex; 
    align-items: flex-start;
    justify-content: space-around;
    padding-top: 60px;
  }
  h2{
    text-align: center;
    padding-top: 60px;
  }
  h3{
    padding: 20px 0;
  }
  p{
    padding-bottom: 30px;
  }
  pre{
    padding-top: 20px;
  }
</style>
