<template>
  <div class="recherche">
    <form v-on:submit.prevent = "recherche()">
        <div class="input-group">
            <md-field class="input-group-field">
                <label>Recherche</label>
                <md-input v-model="uneRecherche"></md-input>
            </md-field>
            <div class="input-group-button"><md-button class="md-raised" v-on:click="recherche"><md-icon>search</md-icon></md-button></div>
        </div>
    </form>
    <h2> Résultats de la recherche</h2>
    <md-table>
        <md-table-row v-for="unFilm in films" v-bind:key="unFilm.key">
            <md-table-cell>{{unFilm.title}}</md-table-cell>
            <md-table-cell><img v-bind:src="'http://image.tmdb.org/t/p/w500/' + unFilm.poster_path" with='100px'></md-table-cell>
            <md-table-cell><md-button v-on:click="voirDetails(unFilm)"><md-icon>visibility</md-icon></md-button></md-table-cell>
        </md-table-row>
    </md-table>        
  </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';
    import axios from 'axios'
import Details from './Details.vue';

    @Component
    export default class Recherche extends Vue {
        baseUrl = 'https://api.themoviedb.org/3/search/movie';
        films = [];
        genres= [];
        uneRecherche = '';
        api_key = '7fccf686b208400fb268558fc6207ce5';

        async recherche() {
            const response = await axios.get(this.baseUrl + '?api_key=' + this.api_key + '&query=' + this.uneRecherche);
            this.films = await response.data.results;
            console.log(this.films);
        }

        voirDetails(film: any) {
            this.$router.push({path: 'details' , query: {
                id: film.id,
                titre: film.title,
                poster_path : film.poster_path,
                backdrop_path : film.backdrop_path,
                details: film.overview,
                genre: film.genres
            }});
        }
    }
</script>
