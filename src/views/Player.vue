<template>
  <div class="player">
    <div class="back" @click="stop">
      <i class="fas fa-long-arrow-left"></i> <span>Retour à la navigation</span>
    </div>
    <div id="player"></div>
  </div>
</template>

<script>
  /*global jwplayer*/
  import data from '@/data.json';

  export default {
    name: "Player",

    data() {
      return {
        data: data,
      }
    },

    mounted() {
      this.play();
    },

    methods: {
      play() {
        const seasonNumber = this.$route.params.season;
        const episodeNumber = this.$route.params.episode;

        console.log(this.data);

        const episode = this.data.seasons[seasonNumber].episodes[episodeNumber];

        let player = jwplayer("player");

        console.log(episode);

        const id = this.id(seasonNumber, episodeNumber);

        let config = {
          title: id + ' - ' + episode.name,
          file: "https://content.jwplatform.com/manifests/yp34SRmf.m3u8",
          //file: episode.stream,
          image: '/img/ep/' + episode.image + '.jpg',
          mediaid: id,
        };

        player.setup(config);
        //player.play();
        //player.setFullscreen(true);
      },

      stop() {
        let player = jwplayer("player");
        player.stop();
        //this.$router.push({ name: 'home' });
        this.$router.back();
      },

      id(season, episode) {
        if (Number(season) < 10) {
          season = '0' + season
        }

        if (Number(episode) < 10) {
          episode = '0' + episode
        }

        return 'S' + season + 'E' + episode;
      }
    }
  }
</script>

