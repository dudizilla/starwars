<template>
  <div>
    <!-- <label class="formLabel" v-if="label" :for="id">{{ label }}</label> -->
    <!-- <div class="inputText"> -->
      <input
        type="text"
        class="input"
        v-model="input"
        :placeholder="placeholder"
      />
    <!-- </div> -->
  </div>
</template>

<script lang="ts">
import { defineComponent, computed } from 'vue'
export default defineComponent({
  components: { },
  props: {
    id: String,
    label: String,
    value: String,
    placeholder: String,
  },
  setup(props, { emit }) {
    const input = computed({
      get: () => props.value,
      set: (value) => emit('update:value', value)
    })
    return {
      input
    }
  }
})
</script>