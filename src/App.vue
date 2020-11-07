<template>
  <div id="app">
    <div class="container">
        <nav>
        </nav>
        <header>
            <div class="banner"></div>
        </header>
        <div class="body">
            <!-- 左側搜尋條件 -->
            <app-filter></app-filter>
            <!-- 右側搜尋結果 -->
            <app-result-list></app-result-list>
        </div>
    </div>
  </div>
</template>

<script>
import AppFilter from './components/AppFilter'
import AppResultList from './components/AppResultList'
export default {
  name: 'App',
  components: {
    AppFilter,
    AppResultList
  }
}
</script>

<style>
@import url("./assets/style/style.css");
</style>
