<template>
  <div id="app">
    <el-container>
      <el-header class="app-header">
        <i>Games World</i>
      </el-header>
      <el-main class="main-container">
        <LandingPage />
      </el-main>
      <el-footer class="app-footer">Made with love</el-footer>
    </el-container>
  </div>
</template>

<script>
import LandingPage from './components/LandingPage';

export default {
  name: 'App',
  components: {
    LandingPage,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.app-header{
  padding: 0px 0px;
  background-color: #9ED8B0;
  display: flex;
  align-items: center;
}
.app-footer {
  border-top: 1px solid #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
}
.main-container{
  min-height: 1000px;
}
</style>
