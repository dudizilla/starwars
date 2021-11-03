<template>
  <div class="home-content">
    <header>
      <h1 id="char-list-title">Star Wars</h1>
      <theme-toggle />
    </header>

    <div class="content">
      <div class="char-list">
        <form>
          <input-text
            id="search-bar"
            placeholder="Search Characters"
            v-model:value="data.filter.name"
            v-on:keyup="searchPeople"
          />
        </form>
        <ul class="list-inner" v-if="data.people.length > 0">
          <Character
            v-for="character in data.people"
            :key="character.url"
            v-bind="{ character }"
            @click="goToInfo(character.url.match(/(?:\d+)/))"
          />
        </ul>

        <div class="nav">
          <Button
            v-if="data.previous"
            class="button--Previous"
            @click="fetchPeople(data.previous)"
            >Previous</Button
          >
          <Button
            class="pagination"
            v-for="n in data.pages"
            :key="n"
            @click="fetchPeople(`https://swapi.dev/api/people/?page=` + n)"
          >
            {{ n }}
          </Button>
          <Button
            v-if="data.next"
            class="button--Next"
            @click="fetchPeople(data.next)"
            >Next</Button
          >
        </div>
        <Loader v-if="data.loading" />
        <router-view />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, watch } from "vue";
import { Filter } from "../models";

import Button from "@/components/Button.vue";
import Character from "@/components/Character.vue";
import InputText from "@/components/InputText.vue";
import Loader from "@/components/Loader.vue";
import ThemeToggle from "@/components/ThemeToggle.vue";
import router from "@/router";

export default defineComponent({
  name: "Home",
  beforeCreate() {
    const dataDefault = "http://swapi.dev/api/people/";
    this.fetchPeople(dataDefault);
  },
  components: {
    Button,
    Character,
    InputText,
    Loader,
    ThemeToggle,
  },
  methods: {
    goToInfo: (userId: number) => {
      router.push({ path: `/people/${userId}` });
    },
  },

  setup() {
    const data = reactive({
      loading: false,
      previous: null,
      pages: 0,
      next: null,
      people: [] as Filter[],
      filter: {
        name: "",
      } as Filter,
    });

    const fetchPeople = (value: any) => {
      data.loading = true;
      const url = value || `http://swapi.dev/api/people/`;

      fetch(url)
        .then((res) => res.json())
        .then((res) => {
          data.loading = false;
          data.next = res.next;
          data.previous = res.previous;
          if (data.next !== null) {
            data.pages = 1;
            data.pages = Math.ceil(res.count / res.results.length);
          }
          data.people = res.results;
        });
    };

    const searchPeople = () => {
      const url = `http://swapi.dev/api/people/?search=${data.filter.name}`;

      fetch(url)
        .then((res) => res.json())
        .then((res) => {
          data.loading = false;
          data.next = res.next;
          if (data.next !== null) {
            data.pages = 1;
            data.pages = Math.ceil(res.count / res.results.length);
          }
          data.people = res.results;
        });
    };

    watch(
      () => data.filter.name,
      () => {
        data.people = [];
        data.loading = true;
      }
    );

    return {
      data,
      fetchPeople,
      searchPeople,
    };
  },
});
</script>
