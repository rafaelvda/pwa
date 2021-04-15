<template>
  <div class="rechercheGenre">
    <form v-on:submit.prevent="rechercheGenre()">
      <div class="input-group">
        <md-field class="input-group-field">
          <label>Recherche par genre</label>
        </md-field>
        <div class="input-group-button"><md-button class="md-raised" v-on:click="rechercheGenre"><md-icon>search</md-icon></md-button></div>
      </div>
    </form>
    <h2>Résultats de la recherche</h2>
    <md-list v-if="montreMoi">
      <md-list-item v-for="unGenre in genres" :key="unGenre">
        {{unGenre}}
      </md-list-item>
    </md-list>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios'

@Component
export default class RechercheGenre extends Vue {
  baseUrl = 'https://api.themoviedb.org/3/movie/top_rated';
  films = [];
  montreMoi = false;
  genres:number[] = [];
  api_key =  '22ed7af5665e4535d05d8796c837c460';

  async rechercheGenre() {
    const response = await axios.get(this.baseUrl +'?api_key='+this.api_key);
    this.films = await response.data.results;
    //console.log(this.films);

    let mesGenres:number[] = [];

    this.films.forEach (function (element) {
      mesGenres.push(element['genre_ids']);
    })

    console.log(this.uniq(mesGenres.flat()));
    this.genres= this.uniq(mesGenres.flat());
    this.montreMoi = true;
  }

  voirDetails(film: any) {
    this.$router.push({ path: 'details', query: {
        id: film.id,
        titre: film.title
      }});
  }

   uniq(a:any) {
    var prims:any = {"boolean":{}, "number":{}, "string":{}}, objs:any[] = [];

    return a.filter(function(item:any) {
      var type = typeof item;
      if(type in prims)
        return prims[type].hasOwnProperty(item) ? false : (prims[type][item] = true);
      else
        return objs.indexOf(item) >= 0 ? false : objs.push(item);
    });
  }

}
</script>


<style scoped>

</style>