<template>
  <div class="well" v-if="history.length > 0">
    <h3 class="headerTitleHst">Arama Geçmişi</h3>
    <ul class="list-group text-left">
      <li class="list-group-item"  v-for="item in history">
        <div>
          <strong>{{ item.from }} > {{ item.to }}</strong>
        </div>
        <br />
        <div>
          <strong class="text-success">{{ item.translateText }}</strong>
          <span class="text-info">{{ item.translatedText }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {

  props : ["history"],

};
</script>

<style>

  @font-face {
    font-family: 'Euclid Circular Regular';
    src: local('Euclid Circular Regular'), local('Euclid-Circular-Regular'),
        url('/fonts/EuclidCircularA-Regular.woff2') format('woff2'),
        url('/fonts/EuclidCircularA-Regular.woff') format('woff'),
        url('/fonts/EuclidCircularA-Regular.ttf') format('truetype');
    font-weight: 400;
    font-style: normal;
  }

 .headerTitleHst {
          font-family: 'Euclid Circular Regular';
          color: black;
  }

</style>
