<template>
    <div id="modal" class="modal-container" @click="closeModal">
        <div id="track-modal" class="content">
            <img :src="track.image">
            <audio id="track" controls>
                <source :src="track.src" type="audio/mpeg">
                Your browser does not support the audio element.
            </audio>
            <div class="track-info">
                <span class="track-title">{{ track.title }}</span>
                <span class="track-artist">{{ track.artist }}</span>
            </div>
            <div class="track-buttons">
                <div class="play-btn" @click="togglePlay">
                    <Play v-if="!playing" />
                    <Pause v-if="playing" />
                </div>

            </div>
        </div>
    </div>
</template>

<script>
import Play from '../assets/images/Play'
import Pause from '../assets/images/Pause'

import { eventBus } from '../main.js'

export default {
    name: 'TrackModal',
    data () {
        return {
            playing: false
        }
    },
    components: {
        Play,
        Pause
    },
    props: [
        'track'
    ],
    methods: {
        closeModal: function(e) {
            let modal = document.getElementById('modal');

            if(e.target === modal) {
                eventBus.$emit('closeModal', false)
            }
        },
        togglePlay: function() {
            if(this.playing == true) {
                this.playing = false;
                document.getElementById('track').pause();
            } else {
                this.playing = true;
                document.getElementById('track').play();
            }
        }
    }
}
</script>

<style scoped>
    .modal-container {
        position: absolute;
        display: flex;
        align-items: center;
        justify-content: center;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        overflow: hidden;
        background: rgba(0,0,0,.5);
        pointer-events: all;
        z-index: 10;
    }

    .content {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 90%;
        max-width: 800px;
        height: 90%;
        background: #fff;
        z-index: 10;
        pointer-events: all;
        overflow-y: scroll;
        scrollbar-width: none;
        border-radius: 1em;
        box-shadow: 0 0 12px rgba(0,0,0,.33);
    }

    .content::-webkit-scrollbar {
        display: none;
    }

    img {
        border-radius: 50%;
        height: 16rem;
        box-shadow: 0 0 9px rgba(0,0,0,.33);
    }

    .track-info {
        display: flex;
        flex-direction: column;
        text-align: center;
        margin: 2rem 0;
    }

    .play-btn {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 5em;    
        width: 5em;
        border-radius: 50%;
        background-color: #42378f;
        background-image: linear-gradient(315deg, #42378f 0%, #f53844 74%);
        box-shadow: 0 0 9px rgba(0,0,0,.33);
        cursor: pointer;
    }

    .play-btn svg {
        width: 50%;
    }

    .play-btn .play {
        margin-left: .45em;
    }

    audio {
        display: none;
    }
</style>