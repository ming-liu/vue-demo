<template lang="html">
  <div class="">
    <MyHeader></MyHeader>
    <div class="articleList">
      <ul>
        <li v-for="i in list">
          <time v-text="$utils.goodTime(i.create_at)"></time>
          <router-link :to="'content/' + i.id">
            {{ i.title }}
          </router-link>
        </li>
      </ul>
    </div>
    <MyFooter></MyFooter>
  </div>
</template>

<script>
import MyHeader from '../components/header.vue'
import MyFooter from '../components/footer.vue'
export default {
  components: {MyHeader, MyFooter},
  data () {
    return {
      list: []
    }
  },
  created () {
    this.loadData()
  },
  methods: {
    loadData () {
      this.$api.get('topics', null, r => {
        this.list = r.data
      })
    }
  }
}
</script>

<style lang="css">
</style>
