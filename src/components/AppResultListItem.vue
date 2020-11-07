<template>
  <div class="result-item spotlight">
    <div class="result-img">
      <a :href="data.tour_detail_url" target="_blank"
        ><img :src="data.image_url" alt=""
      /></a>
    </div>
    <div class="result-body">
      <div class="icon-btns">
        <button class="btn-icon">
          <i class="fas fa-exchange-alt"></i>
        </button>
        <button class="btn-icon">
          <i class="far fa-heart"></i>
        </button>
      </div>
      <p class="result-agency">
        {{ data.agency }}
        <i
          v-for="index in 5"
          :key="index"
          :id="index"
          class="fas fa-star"
          :class="index <= data.rating ? 'text-yellow' : 'text-grey'"
        ></i>
      </p>
      <a :href="data.tour_detail_url" target="_blank"
        ><h3 class="result-title">{{ data.title }}</h3></a
      >
      <div class="result-location">
        <p class="location"><i class="fas fa-map-marker-alt"></i> 花蓮</p>
      </div>
      <div class="result-tags">
        <p v-for="(tag, index) in data.tags" :key="index" class="tag">
          {{ tag }}
        </p>
        <p class="tag">振興三倍券</p>
      </div>
      <div class="result-groups">
        <div
          v-for="(group, index) in data.group"
          :key="index"
          class="result-group"
          :id="group.id"
        >
          <p class="date text-azure">{{ groupDate(group.date) }}</p>
          <p class="party color-azure">可售{{ group.quantity }}位</p>
        </div>
        <!-- <button class="btn-more-group">更多日期</button> -->
      </div>
      <div class="result-price">
        <p>
          <strong class="text-orange big">{{ data.tour_days }}</strong
          >天 <strong class="text-orange big">{{ priceWithComma }}</strong
          >元起
        </p>
        <small
          ><i class="fas fa-coins text-yellow"></i> 下單現賺咖幣
          <span class="text-orange">$595</span> 起</small
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppResultListItem",
  props: {
    data: Object,
  },
  data() {
    return {
      weekDic: {
        Mon: "一",
        Tue: "二",
        Wed: "三",
        Thu: "四",
        Fri: "五",
        Sat: "六",
        Sun: "日",
      },
    };
  },
  computed: {
    priceWithComma() {
      return this.data.min_price.replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
  methods: {
    groupDate(date) {
      const day = new Date(date);
      const dateString = day.toLocaleDateString();
      const result =
        dateString.slice(5) + `(${this.weekDic[day.toString().slice(0, 3)]})`;
      return result;
    },
  },
};
</script>

<style>
</style>