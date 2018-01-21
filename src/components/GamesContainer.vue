<template>
  <div class="games-container">
    <el-row v-if="gamesData.length">
      <el-col :sm="10" :xs="22" :lg="7" :md="10"
          class="card"
          v-for="(game, index) in paginateData[page]"
          :key="index">
        <GameCard :game="game" />
      </el-col>
    </el-row>
    <div v-else>
      No data found!
    </div>
  </div>
</template>

<script>
import GameCard from './GameCard';

export default {
  props: ['gamesData', 'page', 'paginateData'],
  components: {
    GameCard,
  },
};
</script>

<style>
  .games-container {
    margin-top: 20px;
  }
  .card {
    margin: 10px 23px;
  }
</style>
