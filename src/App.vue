<template>
  <div id="app">
    <div class="page-container md-layout-column">
      <md-toolbar class="md-primary">
        <span class="md-title">Pesquisa de Satisfação</span>
        <div class="md-toolbar-section-end">
          <md-button v-on:click="loc.reload()" class="md-accent">Refazer</md-button>
          <md-button v-on:click="res = !res" class="md-accent">Resultado</md-button>
        </div>
      </md-toolbar>
    </div>
    <survey-restaurante-x></survey-restaurante-x>
    <div id="surveyResult" v-show="res"></div>
  </div>
</template>

<script>
import SurveyRestauranteX from "./components/SurveyRestauranteX";

export default {
  name: "app",
  components: {
    SurveyRestauranteX
  },
  data() {
      return {
        res: false,
        loc: window.location
    };
  }
};
</script>

<style src="./theme.scss" lang="scss"></style> 