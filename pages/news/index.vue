<template>
  <div v-if="updateNewsList">
    <LHero title="お知らせ" text="株式会社chatboxの新着情報をお届けします" />
    <CNewsList
      :news-list="newsList"
      :years="years"
      :target-year="targetYear"
      @updateNewsList="updateNewsList"
    />
  </div>
</template>

<script>
import LHero from '@/components/layout/LHero'
import CNewsList from '@/pages/news/-CNewsList'
import { fetchNewsByYear } from '../../service/firebase'
export default {
  components: {
    LHero,
    CNewsList,
  },
  data() {
    return {
      newsList: null,
      targetYear: null,
      years: ['2020', '2021', '2022'],
    }
  },
  mounted() {
    const date = new Date()
    this.targetYear = date.getFullYear()
    this.updateNewsList(this.targetYear)
  },
  methods: {
    async updateNewsList(targetYear) {
      this.targetYear = targetYear
      this.newsList = await fetchNewsByYear(targetYear)
    },
  },
}
</script>

<style lang="scss" scoped></style>
