<template>
  <div class="container">
    <h1 class="text-center headerTitle">Translator</h1>
    <br />
    <div class="row">
      <div class="col-md-12 text-center">
        <translate-form @translatedEvent="translatedText = $event" @historyEvent="history.push($event)" /> <!-- from translateform.vue emit -->
        <h3 class="text-success text-center"> {{ translatedText }} </h3> 
        <search-history :history="history" />
      </div>
    </div>
  </div>
</template>

<script>

import TranslateForm from "./components/TranslateForm";
import SearchHistory from "./components/SearchHistory";

export default {
  components: {
    TranslateForm,
    SearchHistory,
  },

  data() {
    return {
        translatedText : "",
        history : []
    }
  }

};
</script>



<style>

body {
  background-color: #181818;
}

@font-face {
    font-family: 'Euclid Circular Light';
    src: local('Euclid Circular Light'), local('Euclid-Circular-Light'),
        url('/fonts/EuclidCircularA-Light.woff2') format('woff2'),
        url('/fonts/EuclidCircularA-Light.woff') format('woff'),
        url('/fonts/EuclidCircularA-Light.ttf') format('truetype');

    font-weight: 300;
    font-style: normal;
  }

  @font-face {
    font-family: 'Euclid Circular Regular';
    src: local('Euclid Circular Regular'), local('Euclid-Circular-Regular'),
        url('/fonts/EuclidCircularA-Regular.woff2') format('woff2'),
        url('/fonts/EuclidCircularA-Regular.woff') format('woff'),
        url('/fonts/EuclidCircularA-Regular.ttf') format('truetype');
    font-weight: 400;
    font-style: normal;
  }

  body {
     font-family: 'Euclid Circular Light';
  }

  .headerTitle {
          font-family: 'Euclid Circular Regular';
          color: white;
  }
  
</style>
