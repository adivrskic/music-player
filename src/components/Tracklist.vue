<template>
    <div class="content">
        <ul>
            <li v-for="track in tracks" :key="track.title"
                @click="playTrack(track)"
            >
                <div class="container">
                    <span class="track-title">{{ track.title }}</span>
                    <span class="track-artist">{{ track.artist }}</span>
                </div>
                <img class="track-image" :src="track.image">
            </li>
        </ul>
    </div>
</template>

<script>
import { eventBus } from '../main'

export default {
    name: 'Tracklist',
    props: [
        "tracks"
    ],
    methods: {
        playTrack: function(track) {
            console.log(track);
            eventBus.$emit('playTrack', track);
        }
    }
}
</script>

<style>
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

li {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    position: relative;
    padding: 1.5rem;
    border-top: 1px solid #efefef;
    border-bottom: 1px solid #efefef;
    color: #444;
    cursor: pointer;
    overflow: hidden;
    pointer-events: all;
    transition: all .2s ease-in-out;
}

li:hover,
li:focus {
    background: #efefef;
}

li:hover .track-image,
li:focus .track-image {
    opacity: 1;
    height: 180%;
    right: -2.5rem;
}

li:first-of-type {
    border-top: none;
}

li:not(:last-of-type) {
    border-bottom: none;
}

.container {
    display: flex;
    flex-direction: column;
}

.track-title {
    font-size: 1.5rem;
}

.track-artist {
    color: #aaa;
}

.track-image {
    height: calc(80% - 1rem);
    position: absolute;
    right: 1rem;
    border-radius: 50%;
    opacity: .5;
    transition: all .2s ease-in-out;
}

@media screen and (max-width: 480px) {
    li {
        justify-content: center;
        text-align: center;
    }

    li img {
        display: none;
    }
}
</style>