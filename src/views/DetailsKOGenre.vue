<template>
    <div class="details">
        <h1>Details du film</h1>
        <div class= "content">
                <md-steppers>
                    <md-step id="first" md-label="Debut">
                        <md-card>
                            <md-card-content>
                                <h3>{{film.titre}}</h3>
                                <h3>{{film.id}}</h3>
                            </md-card-content> 
                        </md-card>
                        <md-card>
                            <md-card-content v-for="unGenre in film.genre" v-bind:key="unGenre.key">
                                <h3>{{ unGenre.name }}</h3>
                            </md-card-content>
                        </md-card>
                        <md-card>
                            <md-card-content>
                                <img v-bind:src="'http://image.tmdb.org/t/p/w500/' + film.poster_path" with='100px'>
                                <img v-bind:src="'http://image.tmdb.org/t/p/w500/' + film.backdrop_path" with='100px'>
                            </md-card-content>
                        </md-card>
                    </md-step>
                    <md-step id="second" md-label="Suite">
                            <h3> {{film.details}}</h3>
                    </md-step>
                </md-steppers>
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue} from 'vue-property-decorator';

    @Component
    export default class Details extends Vue {
        film: any;

        created() {
            this.film = {
                id: this.$route.query.id,
                titre: this.$route.query.titre,
                poster_path: this.$route.query.poster_path,
                backdrop_path: this.$route.query.backdrop_path,
                details: this.$route.query.details,
                genre: this.$route.query.genre
            };
        }
    }
</script>