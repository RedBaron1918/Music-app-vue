<template>
  <header>
    <h1>My Music</h1>
  </header>
  <main>
    <section class="player">
      <h2 class="song-title">
        {{ current.title }} - <span> {{ current.artist }}</span>
      </h2>
      <div class="controls">
        <button class="prev" @click="prev">
          <i class="fa-solid fa-circle-arrow-left"></i>
        </button>
        <button @click="pause"><i class="fa-solid fa-play"></i></button>
        <button class="next" @click="next">
          <i class="fa-solid fa-circle-arrow-right"></i>
        </button>
      </div>
    </section>
    <section class="playlist">
      <h3>PlayList</h3>
      <button v-for="song in songs" :key="song.src" @click="play(song)">
        {{ song.title }} - {{ song.artist }}
      </button>
    </section>
  </main>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "staying alive",
          artist: "Bee Gees",
          src: require("./assets/stayingalive.mp3"),
        },
        {
          title: "Hold The Line",
          artist: "Toto",
          src: require("./assets/HoldTheLine.mp3"),
        },
        {
          title: "StillStanding",
          artist: "Elton John",
          src: require("./assets/StillStanding.mp3"),
        },
        {
          title: "UnderPressure",
          artist: "Queen & David Bowie",
          src: require("./assets/UnderPressure.mp3"),
        },
        {
          title: "BabyComeBack",
          artist: "Player",
          src: require("./assets/BabyComeBack.mp3"),
        },
        {
          title: "What You Won't Do for Love",
          artist: "Bobby Caldwell ",
          src: require("./assets/WhatYouWontDoForLove.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != undefined) {
        this.current = song;

        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener(
        "ended",
        function () {
          this.next();
        }.bind(this)
      );
      this.isPlaying = true;
    },
    pause() {
      this.isPlaying = !this.isPlaying;
      if (!this.isPlaying) {
        this.player.pause();
      } else {
        this.player.play();
      }
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },

  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    //this.player.play();
  },
};
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
  background-color: #212121;
  color: #fff;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title {
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
}
.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 15px 0;
  padding: 10px;
}
.controls button {
  margin: 10px;
  padding: 10px;
  font-size: 1.4rem;
  border: none;
  background: none;
  cursor: pointer;
}
.controls button:hover {
  background-color: #e5e2e2;
}
.playlist {
  padding: 0px 30px;
}
.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist button {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist button:hover {
  color: #ff5858;
}
.playlist button:active {
  color: #fff;
  background-color: #ff5858;
}
</style>
