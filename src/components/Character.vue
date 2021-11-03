<template>
  <li class="character">
    <div class="character-info">
      <h2 class="character-name">{{ character.name }}</h2>
    </div>
  </li>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { Filter } from '../models/index'
export default defineComponent({
  props: {
    character: {
      type: Object as () => Filter,
      required: true
    }
  }
})
</script>