<template>
  <el-card class="card-body">
    <img :src="getImageSrc(game)">
    <div class="card-details">
      <div class="card-item">
        <strong>Title:</strong><span class="option">{{ game.title }}</span>
      </div>
      <div class="card-item">
        <strong>Platform:</strong><span class="option">{{game.platform}}</span>
      </div>
      <div class="card-item">
        <strong>Genre:</strong><span class="option">{{game.genre}}</span>
      </div>
      <div class="badge-block">
        <div class="score">
          <span class="score-text">{{ game.score }}</span>
        </div>
        <el-tooltip
            placement="bottom"
            content="Editors choice"
            effect="light"
            v-if="game.editors_choice === 'Y'">
          <img src="../assets/editor.png" v-if="game.editors_choice === 'Y'">
        </el-tooltip>
      </div>
    </div>
  </el-card>
</template>

<script>
export default {
  name: 'GameCard',
  props: ['game'],
  methods: {
    getImageSrc(game) {
      let url;
      switch (game.platform) {
        case 'Xbox 360':
          url = require('../assets/xbox.png');
          break;
        case 'PC':
          url = require('../assets/pc.png');
          break;
        case 'PlayStation 3':
          url = require('../assets/playstation3.png');
          break;
        case 'PlayStation Vita':
          url = require('../assets/playstation.png');
          break;
        case 'iPad':
          url = require('../assets/ipad.png');
          break;
        case 'Macintosh':
          url = require('../assets/mac.png');
          break;
        case 'iPhone':
          url = require('../assets/iphone.png');
          break;
        case 'Nintendo 3DS':
        case 'Nintendo DS':
          url = require('../assets/nintendo.png');
          break;
        case 'Android':
          url = require('../assets/android.png');
          break;
        default:
      }
      return url;
    },
  },
};
</script>

<style>
  .card-body{
    height: 260px;
    background-color: #f4f4f5;
  }
  .card-details {
    margin-top: 20px;
    position: relative;
  }
  .card-item {
    display: flex;
  }
  .option {
    display: block;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    margin-left: 10px;
  }
  .badge-block {
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
  }
  .score{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: #9ED8B0;
  }
  .score-text {
    font-size: 26px;
    font-weight: bold;
    color: #fd5e60;
  }
</style>
