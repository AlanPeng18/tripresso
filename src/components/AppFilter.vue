<template>
  <aside class="column-1-4">
    <button class="btn-share">
      <i class="fas fa-share-alt"></i><span> 分享搜尋結果</span>
    </button>
    <div class="filters">
      <div class="filter filters-title">
        <h4 class="filter-title">篩選項目</h4>
      </div>
      <div class="filter">
        <button class="filter-caret"><i class="fas fa-angle-up"></i></button>
        <div class="filter-title">
          <i class="fas fa-calendar-week"></i>
          <p class="filter-title">出發日期</p>
        </div>
        <div class="filter-body">
          <input
            class="input-date"
            type="date"
            min="2020-11-07"
            name="departureDateStart"
            id="departureDateStart"
            value="2020-11-07"
          />
          <span>~</span
          ><input
            class="input-date"
            type="date"
            min="2020-11-07"
            name="departureDateEnd"
            id="departureDateEnd"
            value="2020-11-07"
          />
        </div>
      </div>
      <div class="filter">
        <button class="filter-caret"><i class="fas fa-angle-up"></i></button>
        <div class="filter-title">
          <i class="far fa-compass"></i>
          <p class="filter-title">目的地</p>
        </div>
        <div class="filter-body">
          <div class="form-control">
            <input type="checkbox" name="mainLandChina" id="mainLandChina" />
            <label for="mainLandChina">港澳中國</label>
          </div>
        </div>
      </div>
      <div class="filter">
        <button class="filter-caret"><i class="fas fa-angle-up"></i></button>
        <div class="filter-title">
          <i class="far fa-clock"></i>
          <p class="filter-title">天數</p>
        </div>
        <div class="filter-body">
          <div class="form-control">
            <input type="checkbox" name="belowFiveDays" id="mainLandChina" />
            <label for="belowFiveDays">5天以下</label>
          </div>
          <div class="form-control">
            <input type="checkbox" name="SixToEightDays" id="mainLandChina" />
            <label for="SixToEightDays">6-8天</label>
          </div>
        </div>
      </div>
      <div class="filter">
        <button class="filter-caret"><i class="fas fa-angle-down"></i></button>
        <div class="filter-title">
          <i class="fas fa-flag"></i>
          <p class="filter-title">成團狀態</p>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
    name: 'AppFilter'
};
</script>

<style>
</style>