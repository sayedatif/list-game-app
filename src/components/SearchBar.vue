<template>
  <div>
    <el-autocomplete
        v-model="search"
        valueKey="title"
        class="search-input"
        placeholder="Search for games"
        :fetch-suggestions="querySearch"
        @select="handleSelect"></el-autocomplete>
    <div class="filter-block">
      Filter By
      <div class="filters">
        <el-checkbox v-model="filterByScore" @change="handleScorefilter">Score</el-checkbox>
        <el-radio-group
            v-model="radio"
            v-if="filterByScore"
            class="radio-group"
            @change="handleScorefilter">
          <el-radio label="asc">Ascending</el-radio>
          <el-radio label="desc">Descending</el-radio>
        </el-radio-group>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      filterByScore: false,
      radio: 'asc',
    };
  },
  props: ['gamesData'],
  methods: {
    querySearch(value, cb) {
      const data = this.gamesData;
      const results = value ? data.filter(this.findQuery(value)) : data;
      cb(results);
    },
    findQuery(queryString) {
      return game => (game.title.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
    },
    handleSelect(value) {
      // console.log('value', value);
    },
    handleScorefilter(value) {
      if (value) {
        this.$emit('filterByScore', this.radio);
      }
    },
  },
};
</script>

<style>
  .search-input {
    display: flex;
  }
  .filter-block {
    display: flex;
    margin-top: 5px;
    margin-bottom: 5px;
  }
  .filters {
    margin-left: 20px;
  }
  .radio-group{
    margin-left: 10px;
  }
  .el-checkbox__input.is-checked .el-checkbox__inner, .el-checkbox__input.is-indeterminate .el-checkbox__inner {
    background-color: #9ED8B0;
    border-color: #9ED8B0;
  }
  .el-checkbox__input.is-checked+.el-checkbox__label {
    color: #9ED8B0;
  }
  .el-radio__input.is-checked .el-radio__inner {
    background-color: #9ED8B0;
    border-color: #9ED8B0;
  }
  .el-radio__input.is-checked+.el-radio__label {
    color: #9ED8B0;
  }
</style>
