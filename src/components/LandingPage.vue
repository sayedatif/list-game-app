<template>
  <div v-loading="loading">
    <el-row type="flex" justify="center">
      <el-col :lg="20" :xs="24">
        <SearchBar v-bind:games-data="gamesData" v-on:filterByScore="filterByScore" />
        <GamesContainer
            v-bind:games-data="gamesData"
            v-bind:page="page"
            v-bind:paginate-data="paginateData" />
        <div class="paginator">
          <el-pagination
            v-if="gamesData.length"
            background
            @current-change="handleChange"
            layout="prev, pager, next"
            :total="gamesData.length">
          </el-pagination>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './SearchBar';
import GamesContainer from './GamesContainer';
import fallback from '../fallback.json';

export default {
  name: 'LandingPage',
  components: {
    SearchBar,
    GamesContainer,
  },
  data() {
    return {
      page: 10,
      loading: false,
      gamesData: [],
      paginateData: {},
    };
  },
  created() {
    this.fetchRemoteData();
  },
  methods: {
    fetchRemoteData() {
      this.loading = true;
      return axios.get('http://starlord.hackerearth.com/gamesaren')
        .then((result) => {
          this.loading = false;
          this.gamesData = result.data.filter(data => data.title);
          this.makeArrayChunks(this.gamesData);
        }).catch(() => {
          this.loading = false;
          this.gamesData = fallback.filter(data => data.title);
          this.makeArrayChunks(this.gamesData);
        });
    },
    makeArrayChunks(data) {
      const paginateObj = {};
      const chunkSize = 12;
      const pageSize = 10;
      for (let i = 0; i < data.length; i += pageSize) {
        paginateObj[i + pageSize] = data.slice(i, i + chunkSize);
      }
      this.paginateData = paginateObj;
    },
    handleChange(value) {
      this.page = 10 * value;
    },
    filterByScore(order) {
      function compare(a, b) {
        if (a.score < b.score) {
          return -1;
        }
        if (a.score > b.score) {
          return 1;
        }
        return 0;
      }
      let sort = this.gamesData.sort(compare);
      if (order === 'desc') {
        sort = sort.reverse();
      }
      this.makeArrayChunks(sort);
    },
  },
};
</script>

<style>
.paginator {
  margin-top: 10px;
}
.el-pagination.is-background .el-pager li.active {
  background-color: #9ED8B0;
}
</style>
