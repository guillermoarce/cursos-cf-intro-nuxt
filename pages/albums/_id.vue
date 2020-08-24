<template>
    <div class="container">
        <header>
            <nuxt-link to="/">Regresar</nuxt-link>        
            <h1 class="title">{{ album.title}}</h1>
        </header>
        <div class="columns is-multiline">
            <div class="column is-one-quarter" v-for="photo in photos" :key="photo.id">
                <img :src="photo.url" :alt="photo.title">
            </div>
        </div>
    </div>
</template>
<script>
import router from 'vue-router';
import axios from 'axios';
import env from '../../config/env';
export default {
    name: 'AlbumIndvPage',
    data() {
        return {
            album: {},
            photos: []
        }
    },
    created: async function (){
        let albumId = this.$route.params.id;

        let albumResponse = await axios.get(`${env.endpoint}/albums/${albumId}`);
        this.album = albumResponse.data;

        let photoResponse = await axios.get(`${env.endpoint}/albums/${albumId}/photos`);
        this.photos = photoResponse.data;

        /* let albumId = this.$route.params.id;
        axios.get(`${env.endpoint}/albums/${albumId}`)
            .then(resp => {
                this.album = resp.data;
            });
        axios.get(`${env.endpoint}/albums/${albumId}/photos`)
            .then(resp => {
                this.photos = resp.data;
            });  */   
    }
}
</script>

<style scoped>
.container{
    text-align: center;
}
</style>