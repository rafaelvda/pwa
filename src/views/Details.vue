<template>
    <div class="details" v-if="estPres">
        <h1>Details du film</h1>
        <div class="content">
            <md-steppers md-alternative>
                <md-step id="premier" md-label="Début">
            <md-card class="details-card">
                <h3>{{film.titre}}</h3>
                <h3>{{film.id}}</h3>
                {{ detailFilm.release_date}}
            </md-card>
            <md-table>
            <md-table-row v-for="unGenre in genres" v-bind:key="unGenre.key">
                <md-table-cell>{{unGenre.name}}</md-table-cell>
            </md-table-row>
            </md-table>
           <md-card-media alt="image de devant" >
                <img v-bind:src="'http://image.tmdb.org/t/p/w500/' +detailFilm.poster_path" width='100px' alt="Pas beau" >
            </md-card-media>
            <md-card-media alt="image de derrière">
                <img  v-bind:src="'http://image.tmdb.org/t/p/w500/' +detailFilm.backdrop_path" width='100px'  alt="Pas beau">
            </md-card-media>
                </md-step>
              <md-icon>details</md-icon>

                <md-step id="second" md-label="Suite">
                    <md-card class="details-card">
                        {{ detailFilm.overview}}
                        {{ creditFilm.cast}}
                    </md-card>
                </md-step>

              <md-step id="third" md-label="Cast">

              </md-step>

            </md-steppers>
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';
    import axios from 'axios';

    @Component
    export default class Details extends Vue {
        film: any;
        baseUrl = 'https://api.themoviedb.org/3/movie/';
        query = '';
        api_key =  '22ed7af5665e4535d05d8796c837c460';
        genres = [];
        detailFilm= null ;
        estPres=false ;
        compagnies = [] ;
        creditFilm = [];

        created() {
            this.film = {
                id: this.$route.query.id,
                titre: this.$route.query.titre
            };
            this.cherchedetail()
        }

        mounted(){
        }

        async cherchedetail() {
            //const response = await axios.get(this.baseUrl + `/search.json?title=${this.query}`);
            const response = await axios.get(this.baseUrl + this.film.id + '?api_key='+this.api_key);
            this.genres = await response.data.genres;
            this.detailFilm = await response.data ;

            //pour le cast
            const num2 = await axios.get(this.baseUrl + this.film.id + '/credits?api_key='+this.api_key);
            this.creditFilm = await num2.data ;

            console.log(this.detailFilm) ;
            this.estPres = true ;
        }

    }
</script>

<style>
    .content {
        display: flex;
        justify-content: center;
    }

    .details-card {
        max-width: 800px;
        padding: 1rem 2rem;
    }

    .details-card p {
        padding-left: 2rem;
    }
</style>