<template>
  <div class="select">
    <p class="select-selected">{{modelValue}}</p>
    <ul class="select-options">
      <li 
        class="select-option"
        v-for="{name, value} in options"
        :key='value'
        @click="selectOption({name, value})"
      >{{name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array, 
      default() {
        return []
      } 
    },
    modelValue : null
  },
  methods: {
    selectOption (value) {
      this.$emit("update:opt", value)
    }
  }
}
</script>

<style>

</style>