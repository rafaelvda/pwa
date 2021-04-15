<template>
  <div id="app">
    <md-toolbar color="primary" class="expanded-toolbar">
      <span class="enc">
        <md-button><router-link to="/"><md-icon>home</md-icon></router-link></md-button>
      </span>
      <md-menu md-direction="bottom-start">
        <md-button md-menu-trigger><md-icon>menu</md-icon></md-button>
        <md-menu-content>
          <md-menu-item><router-link to="/recherche">Recherche</router-link></md-menu-item>
          <md-menu-item><router-link to="/rechercheGenre">Recherche par genre</router-link></md-menu-item>
        </md-menu-content>
      </md-menu>
    </md-toolbar>
    <router-view/>
  </div>
</template>

<style>
  #app {
    font-family: 'Gill Sans Ultra Bold', sans-serif;
  }
  .enc {
    flex: 1;
    text-align: left;
  }
  h1 {
    text-align: center;
  }
</style>
