<template>
  <div class="info-content">
    <header>
      <button id="search-button" @click="goToHome()">
        <svg id="search-icon" class="search-icon" viewBox="0 0 24 24">
          <path
            d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"
          />
          <path d="M0 0h24v24H0z" fill="none" />
        </svg>
      </button>
      <h1 id="char-info-title">Star Wars</h1>
      <theme-toggle />
    </header>
  </div>
  <div class="char-content">
    <div class="card">
      <img src="@/assets/logo.png" />
      <div class="infos">
        <p id="char-name">
          <b>{{ char.name }}</b>
        </p>
        <p v-if="char.height != 'unknown'">
          <b>Height:</b> {{ char.height }}cm
        </p>
        <p v-if="char.mass != 'unknown'"><b>Mass:</b> {{ char.mass }}kg</p>
        <p v-if="char.birth_year != 'unknown'">
          <b>Birth year:</b> {{ char.birth_year }}
        </p>
        <p v-if="char.gender != 'n/a'"><b>Gender:</b> {{ char.gender }}</p>
      </div>
    </div>
    <h1>Movies</h1>
    <li
      class="movies"
      v-for="film in char.filmsName"
      :key="film.filmsName"
      v-bind="{ film }"
    >
      {{ film }}
    </li>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";

import ThemeToggle from "@/components/ThemeToggle.vue";
import router from "@/router";

export default defineComponent({
  name: "CharacterInfo",
  components: {
    ThemeToggle,
  },

  methods: {
    goToHome: () => {
      router.replace({ path: "/" });
    },
  },

  setup() {
    const char = reactive({
      name: null,
      height: null,
      mass: null,
      birth_year: null,
      gender: null,
      filmsName: [] as any,
    });

    const getCharacterInfo = (path: string) => {
      const url = `http://swapi.dev/api${path}`;
      fetch(url)
        .then((res) => res.json())
        .then((res) => {
          char.name = res.name;
          char.height = res.height;
          char.mass = res.mass;
          char.birth_year = res.birth_year;
          char.gender = res.gender;
          getMoreInfo(res.films);
        });
    };

    const getMoreInfo = (film: any) => {
      for (let i = 0; i < film.length; i++) {
        const url = `${film[i]}`;
        fetch(url)
          .then((res) => res.json())
          .then((res) => {
            char.filmsName.push(res.title);
          });
      }
    };

    getCharacterInfo(window.location.pathname);
    return {
      getCharacterInfo,
      getMoreInfo,
      char,
    };
  },
});
</script>
