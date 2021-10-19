<template>
  <div class="background">
    <div class="top-buttons">
      <div class="characters-list-button">
        <button class="characters-list">
          <img id="characters-list" src="" alt="list icon">
        </button>
      </div>
      <div class="theme-toggle">
        <input id="toggle" class="toggle" type="checkbox">
        <label for="toggle"></label>
      </div>
    </div>
    <div class="main-component">
      <div class="logo">
        <h1>Star Wars</h1>
        <h2>Characters Search</h2>
      </div>
      <div class="search-bar">
        <input type="text" id="search-bar" placeholder="type here the character name">
        <img src="" alt="magnifying glass icon">
      </div>
      <div class="search-button">
       <button id="search-button">
         search
       </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<style scoped>
  .background {
    background-color: #fafbff;
    border: 1.5px solid #2ff924;
    border-top: 0;
    border-bottom: 0;
    width: 100%;
    justify-content: center;
  }

  .top-buttons {
    padding: 24px;
    width: 100%;
  }

  .characters-list {
    background-color: #fafbff;
    border: 1.5px solid #2ff924;
    width: 24px;
    height: 24px;
    border-radius: 4px;
    outline: none;
  }

  .characters-list:hover {
    transition: border 0.25s ease-in;
    border: 2.5px solid #2ff924;
  } 

  .toggle {
    display: none;
  }

  .toggle + label {
    width: 36px;
    height: 24px;
    background-color: #888888;
    display: block;
    position: relative;
    border-radius: 20px;
    padding: 2px;
    transition: 200ms;
  }

  .toggle + label:before {
    content: '';
    position: absolute;
    width: 24px;
    height: 24px;
    background-color: #ff0000;
    display: block;
    border-radius: 50%;
    right: unset;
    left: 2px;
    top: 2px;
    transition: 200ms;
  }

  .toggle:checked + label {
    background-color: #efefef;
  }

  .toggle:checked + label::before {
    content: '';
    background-color: #2ff924;
    left: calc(100% - 22px);
    box-shadow: 0 4px 4px rgb(0, 0, 0/ 10%);
  }

  h1 {
    font-size: 48px;
  }

  h2 {
    font-size: 20px;
    font-weight: 400;
  }

  #search-bar {
    font-family: 'Montserrat', sans-serif;
    font-weight: 300;
    height: 35px;
    width: 75%;
    background-color: #fafbff;
    border: 1.5px solid #2ff924;
    border-radius: 20px;
    text-indent: 10px;
    outline: none;
  }

  #search-bar:hover {
    transition: border 0.25s ease-in;
    border: 2.5px solid #2ff924;
  }

  #search-button {
    background-color: #fafbff;
    border: 1.5px solid #2ff924;
    max-width: 100px;
    font-family: 'Star Jedi', arial;
  }

  #search-button:hover {
    transition: border 0.25s ease-in;
    border: 2.5px solid #2ff924;
  }
</style>
