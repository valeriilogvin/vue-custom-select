<template>
  <div class="select">
    <p 
      v-if="!isMultiple"
      class="select-selected"
      @click="isOptionsVisible = !isOptionsVisible"
    >
      {{modelValue.name || 'Select option'}}
    </p>
    <p 
      v-else
      class="select-selected"
      @click="isOptionsVisible = !isOptionsVisible"
    >
      <span v-if="!modelValue.length">Select option</span>
      <span v-else>Selected {{modelValue.length}} option</span>
    </p>


    <ul v-if="isSearchable" class="select-options" v-show="isOptionsVisible">
      <input 
        placeholder="Search"
        class="select-input" 
        type="text" 
        v-model='searchValue'
      >
      <li 
        class="select-option"
        v-for="{name, value} in filteredItems"
        :key='value'
        @click="selectOption({name, value})"
      >{{name}}</li>
    </ul>

    <ul v-else class="select-options" v-show="isOptionsVisible">
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
    modelValue : {
      type: Object,
      default() {
        return {}
      }
    },
    isMultiple: {
      type: Boolean,
      default() {
        return false
      }
    },
    isSearchable: {
      type: Boolean,
      default() {
        return false
      }
    }
  },
  data () {
    return {
      isOptionsVisible: false,
      searchValue: ''
    }
  },
  methods: {
    selectOption (obj) {
      if(this.isMultiple) {
        const arr = this.modelValue
        const idx = arr.findIndex(d => d.value === obj.value)

        if (idx >= 0) {
          arr.splice(idx, 1)
          this.$emit("update:modelValue", arr)
          this.hideOptions()
        } else {
          arr.push(obj)
          this.$emit("update:modelValue", arr)
          this.hideOptions()
        }
        return
      }
      this.$emit("update:modelValue", obj)
      this.hideOptions()
    },
    hideOptions() {
      this.isOptionsVisible = false
    }
  },
  computed: {
    filteredItems() {
      return this.options.filter(item => {
         return item.name.toLowerCase().indexOf(this.searchValue.toLowerCase()) > -1
      })
    }
  }
}
</script>

<style>
  .select{
    width: 100%;
    min-width: 250px;
    max-width: 350px;
    position: relative;
  }
  .select-selected,
  .select-options{
    font-size: 18px;
    line-height: 22px;
    padding: 15px 20px;
    background: rgba(247, 247, 247, 0.06);
    border: 1px solid rgba(255, 255, 255, 0.4);
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    backdrop-filter: blur(6px);
    border-radius: 10px;
  }

  .select-selected{
    cursor: pointer;
    user-select: none;
  }

  .select-options{
    position: absolute;
    width: 100%;
    bottom: -10px;
    left: 0;
    transform: translateY(100%);
    z-index: 1;
  }
  .select-option{
    list-style: none;
    cursor: pointer;
    transition: color .2s ease;
  }

  .select-option:hover{
    color: #22C50C;
  }

  .select-multiple-selected + .select-multiple-selected{
    margin-left: 15px;
  }
  .select-option + .select-option {
    margin-top: 10px;
  }

  .select-input{
    width: 100%;
    background: none;
    outline: none;
    font-size: 18px;
    line-height: 22px;
    border: 1px solid rgba(255, 255, 255, 0.4);
    border-radius: 10px;
    color: #fff;
    padding: 10px;
    margin-bottom: 10px;
  }
</style>