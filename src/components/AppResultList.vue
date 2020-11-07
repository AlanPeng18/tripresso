<template>
  <section class="column-3-4">
    <div class="result-summary">
      <h2>
        <strong class="big">台灣旅遊 </strong
        ><span class="text-blue">130</span> 個行程，平均團費
        <span class="text-blue">4,493</span> 元
      </h2>
    </div>
    <div class="result-sort">
      <p class="sort-title">排序</p>
      <div class="sort-btns">
        <button
          class="btn-sort"
          :class="{ 'btn-sort--active': isSortByRating }"
          @click="sortByRating('rating_desc')"
        >
          精選評分
        </button>
        <button
          class="btn-sort sort-price"
          :class="{ 'btn-sort--active': isSortByPrice }"
          @click="showSortPrice = !showSortPrice"
          @blur="blurShowSortPrice($event)"
        >
          價格 <i class="fas fa-caret-down"></i>
          <ul :class="{ show: showSortPrice }">
            <li>
              <button id="priceAsc" @click="sortByPrice('price_asc')">
                價格：低至高
              </button>
            </li>
            <li>
              <button id="priceDesc" @click="sortByPrice('price_desc')">
                價格：高至低
              </button>
            </li>
          </ul>
        </button>
        <button class="btn-sort">天數 <i class="fas fa-caret-down"></i></button>
        <button class="btn-sort">出發日期</button>
      </div>
    </div>
    <div class="result">
      <app-result-list-item
        v-for="(item, index) in currentList"
        :key="index"
        :data="item"
      ></app-result-list-item>
    </div>
    <div class="pager">
      <button
        class="btn-page"
        :class="{ 'btn-page--disabled': currentPage == 1 }"
        :disabled="currentPage == 1"
        @click="changePage(currentPage - 1)"
      >
        <i class="fas fa-chevron-left"></i>
      </button>
      <button
        v-for="index in 5"
        :key="index"
        class="btn-page"
        :class="{ 'btn-page--active': index + minPager - 1 == currentPage }"
        @click="changePage(index + minPager - 1)"
      >
        {{ index + minPager - 1 }}
      </button>
      <button
        class="btn-page"
        :class="{ 'btn-page--disabled': currentPage == totalPage }"
        :disabled="currentPage == totalPage"
        @click="changePage(currentPage + 1)"
      >
        <i class="fas fa-chevron-right"></i>
      </button>
    </div>
  </section>
</template>

<script>
import AppResultListItem from "./AppResultListItem";
export default {
  name: "AppResultList",
  components: {
    AppResultListItem,
  },
  data: function () {
    return {
      rowPerPage: 15,
      showSortPrice: false,
      pagerToShow: 5,
      currentPage: 1,
      pagerActiveIndex: 3,
      minPager: 1,
      currentSortion: "rating_asc",
      sortType: "rating",
      totalCount: 0,
      totalPage: 0,
      currentList: [],
    };
  },
  created() {
    //先取得總筆數
  },
  mounted() {
    const vm = this;
    let getTotalCount = this.search(0, 1000, this.currentSortion);
    let firstLoad = this.search(1, this.rowPerPage, "rating_asc");
    Promise.all([getTotalCount, firstLoad]).then((result) => {
      vm.totalCount = result[0].tour_list.length;
      vm.updateList(result[1]);
      vm.setPager(1);
      this.totalPage = Math.ceil(this.totalCount / this.rowPerPage);
    });
  },
  methods: {
    //搜尋
    async search(page, rowPerPage, sortion) {
      const data = await fetch(
        `http://interview.tripresso.com/tour/search?page=${page}&row_per_page=${rowPerPage}&sort=${sortion}`
      )
        .then((res) => res.json())
        .then((data) => data.data)
        .catch((error) => {
          console.log(error);
          return { tour_list: [] };
        });
      return data;
    },
    //更新結果列表
    updateList(data) {
      this.currentList = data.tour_list;
    },
    //設定分頁
    setPager(currentPage) {
      if (currentPage < 3) {
        this.minPager = 1;
      } else if (currentPage > this.totalPage - 2) {
        this.minPager = this.totalPage - 4;
      } else {
        this.minPager = currentPage - 2;
      }
      this.pagerActiveIndex = currentPage;
    },
    //換頁
    changePage(page) {
      this.currentPage = page;
      const vm = this;
      this.search(page, this.rowPerPage, this.currentSortion).then((data) => {
        vm.updateList(data);
        vm.setPager(page);
      });
      //滾動到最上面
      window.scrollTo(0, 0);
    },
    //照價格排序
    sortByPrice(sortion) {
      this.currentSortion = sortion;
      this.currentPage = 1;
      const vm = this;
      this.search(1, this.rowPerPage, sortion).then((data) => {
        vm.updateList(data);
        vm.setPager(1);
      });
    },
    //照評價排序
    sortByRating(sortion) {
      this.currentSortion = sortion;
      this.currentPage = 1;
      const vm = this;
      this.search(1, this.rowPerPage, sortion).then((data) => {
        vm.updateList(data);
        vm.setPager(1);
      });
    },
    //隱藏價格下拉選單
    blurShowSortPrice(event) {
      if (
        event.relatedTarget == null ||
        (event.relatedTarget.id != "priceAsc" &&
          event.relatedTarget.id != "priceDesc")
      ) {
        this.showSortPrice = false;
      }
    },
  },
  computed: {
    isSortByRating() {
      return (
        this.currentSortion === "rating_asc" ||
        this.currentSortion == "rating_desc"
      );
    },
    isSortByPrice() {
      return (
        this.currentSortion === "price_asc" ||
        this.currentSortion == "price_desc"
      );
    },
  },
};
</script>

<style>
</style>