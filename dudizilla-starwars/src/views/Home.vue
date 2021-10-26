<template>
    <main class="root">
      <header class="header">
          <h1 class="title">Star Wars</h1>
        </header>

      <section class="list">
        <div class="content">
          <form>
            <input-text id="search-bar"
              placeholder="Search Characters"
              v-model:value="data.filters.name" v-on:keyup="searchPeople"
            />
          </form>
        <ul class="list-inner" v-if="data.people.length > 0">
          <Character
            v-for="character in data.people"
            :key="character.url"
            v-bind="{ character }"
          />
        </ul>

        <div class="error" v-else-if="!data.loading">
          <h2 class="error-title">Nothing found</h2>
          <p class="error-text">
            These are not the characters you are searching for.
          </p>
        </div>

        <Loader v-if="data.loading" />
        <Button v-else-if="data.next" class="button--Load" @click="fetchPeople"
          >Load more</Button
        >
        </div>
      </section>
    </main>
</template>

<script lang="ts">
import { defineComponent, reactive, watch } from 'vue'
import { Filter, CharacterType } from '../../types'

import Loader from '../components/partials/Loader/Loader.vue'
import InputText from '../components/forms/InputText/InputText.vue'
import Button from '../components/forms/Button/Button.vue'
import Character from '../components/list/Character.vue'

export default defineComponent({
  name: 'Home',
  components: {
    Loader,
    InputText,
    Button,
    Character,
  },

  setup() {
    const data = reactive({
      loading: false,
      showList: false,
      next: null,
      people: [] as CharacterType[],
      filters: {
        name: ''
      } as Filter
    })

    const fetchPeople = () => {
      data.loading = true
      const url = data.next || `http://swapi.dev/api/people/`
      fetch(url)
        .then((res) => res.json())
        .then((res) => {
          data.loading = false
          data.next = res.next
          data.people.push(...res.results)
        })
    }
    
    fetchPeople()
    const searchPeople = () => {
      const url = `http://swapi.dev/api/people/?search=${data.filters.name}`
      fetch(url)
        .then((res) => res.json())
        .then((res) => {
          data.loading = false
          data.next = res.next
          data.people = res.results
        })
    }

    watch(
      () => data.filters.name,
      () => {
        data.people = []
        data.loading = true
      }
    )

    return {
      data,
      fetchPeople,
      searchPeople
    }
  }
})
</script>
