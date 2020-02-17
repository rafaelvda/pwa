<template>
    <div class="details">
        <h1>Details du film</h1>
        <div class="content">
            <md-card class="details-card">
                <h3>{{film.titre}}</h3>
                <h3>{{film.id}}</h3>
            </md-card>
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';

    @Component
    export default class Details extends Vue {
        film: any;

        created() {
            this.film = {
                id: this.$route.query.id,
                titre: this.$route.query.titre
            };
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