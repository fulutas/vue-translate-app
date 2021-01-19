<template>
  <form @submit.prevent="translateIt" class="well">
    <textarea
      v-model="translateText"
      cols="30"
      rows="5"
      class="form-control"
      placeholder="Çevirmek istediğiniz kelime/cümle yazınız."
    ></textarea>
    <br>
    <div class="text-left chsLang">
      <strong>Dil Seç : </strong>
    </div>
    <select v-model="translateTo" class="form-control">
      <option v-for="(value, key) in languages" :value="key">{{ value }}</option>
    </select>
    <br />
    <div class="text-left" v-if="perceivedLang"> <!-- veri var ise gösterir -->
      <strong>Algılanan Dil : </strong> {{ perceivedLang }}
    </div>
    <br />
    <div>
    <button type="submit" class="btn btn-success  btn-block translatebtn">
      Çevir
    </button>
      {{errorMsg}}
    </div>
  </form>
</template>

<script>

import axios from "axios";

export default {
  data(){
      return {
        translateText : "",
        translateTo : "",
        languages : {},
        perceivedLang : "",
        errorMsg : "",
      }
  },

  methods : {

      // text translate submit click
      translateIt(){

        let url = "https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20181002T212402Z.845255b7ffa94333.9ec78bf8282c3d1446a9e98dfd3ae4158618eab4&text=" + this.translateText + "&lang=" + this.translateTo
          
          axios.get(url)
          .then(response => {

              this.perceivedLang = this.languages[this.translateTo] // algılanan dil açıklaması alır
              this.$emit("translatedEvent", response.data.text[0]) // çevirisi yapılan cümleyi gönderir


              // from : data.lang:"tr-en" api objesinden tutulur. (1. from 2. to)
              let history = {
                from : this.languages[response.data.lang.split("-")[0]],
                to : this.perceivedLang,
                translateText : this.translateText,
                translatedText : response.data.text[0],
              }

              // app.vue comp data'yı gönderir.
              this.$emit("historyEvent", history);

              // click sonrası textarea,select ve dil text temizler
              this.translateTo = "",
              this.translateText = "",
              this.perceivedLang = ""

          }). catch(e => console.log(e))
      }
  },

  // API'dan desteklenen dil seçenekleri
  created(){
    axios.get("https://translate.yandex.net/api/v1.5/tr.json/getLangs?key=trnsl.1.1.20181002T212402Z.845255b7ffa94333.9ec78bf8282c3d1446a9e98dfd3ae4158618eab4&ui=tr")
    .then(response => {
      this.languages = response.data.langs;
x    })
    .catch(e => this.errorMsg = e);
  }
};
</script>

<style>

textarea {
  resize: horizontal
}

.translatebtn{
  width: 30%;
  margin: auto;
}

.chsLang{
  margin-bottom: 10px;
}

</style>
