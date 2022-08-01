<template>
  <div>
    <div id="app">
      <header>
        <h1>My music</h1>
      </header>
      <main>
        <section class="player">
          <h2 class="song-title">{{ current.title }} - <span>{{ current.arttist }}</span> </h2>
          <div class="control">
            <button class="prev" @click="prev">Prev</button>
            <button class="play" @click="play">Play</button>
            <button class="pausa" @click="pause">Pausa</button>
            <button class="next" @click="next">Next</button>
          </div>
        </section>
        <section class="playlist">
          <h3>Music</h3>
          <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src)
          ? 'song playing' : 'song'">
            {{ song.title }} - {{ song.arttist }}
          </button>
        </section>
      </main>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
         {
          title: 'Sakit Samedov',
          arttist: 'roza-roza',
          src: require('../assets/sakit_samedov_-_roza_roza_(z2.fm).mp3')
        },
        {
          title: 'Pro Barmen',
          arttist: 'Elsen',
          src: require('../assets/Elsen Pro-Barmen (dodasi.com).mp3')
        },
        {
          title: 'Karman',
          arttist: 'Tural_Everest_Ruslan',
          src: require('../assets/Tural_Everest_Ruslan_Dobryj_Karman.mp3')
        },
        {
          title: 'Jalolidi Ahmadaliyev',
          arttist: 'Ha joningdan',
          src: require('../assets/jaloliddin-ahmadaliyev-qarasang-qarab-qoy-ha-joningdan_(uzhits.net).mp3')
        },
        {
          title: 'Sakit Samedov',
          arttist: 'chaki chaki',
          src: require('../assets/sakit_samedov_-_chaki_chaki_boroni_(z2.fm).mp3')
        },

      ],
      player: new Audio()
    }
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;

        this.player.src = this.current.src
      }
      this.player.play();
      this.player.addEventListener('ended', function () {
        this.index++;
        if (this.index < 0) {
          this.index = this.songs.length - 1;
        }

        this.current = this.songs[this.index];
        this.play(this.current)
      }.bind(this));
      this.isPlaying = true
    },
    pause() {
      this.player.pause()
      this.isPlaying = true
    },
    prev() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    },
    next() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    }
  },
  created() {
    this.current = this.songs[this.index]
    this.player.src = this.current.src

  },
}
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #333;
  color: #fff;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
  background-color: rgb(189, 189, 202);
  height: 800px;
}

.song-title {
  color: #212121;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;
}

.control {
  display: flex;
  justify-content: center;
  padding: 30px 15px;
  align-items: center;
}

button {
  appearance: none;
  background: none;
  border: none;
  cursor: pointer;
}

.play {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 10px;
  color: #fff;
  background-color: rgb(8, 169, 8);
}

button:hover {
  opacity: 0.8;
}

.pausa {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 10px;
  color: #fff;
  background-color: red;
}

.next,
.prev {
  font-size: 15px;
  font-weight: 700;
  padding: 5px 15px;
  margin: 0px 15px;
  border-radius: 10px;
  color: #fff;
  background-color: rgb(109, 109, 109);
}

.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 700;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
  /* background-color: greenyellow; */
}

.playlist .song:hover {
  color: #fff;
}

.playlist .song.playing {
  color: #fff;
  background-color: #212121;
}
</style>
