<template lang="html">
  <div class="">
    <MyHeader></MyHeader>
    <h2 v-text="dat.title"></h2>
    <p>作者：{{dat.author.loginname}}　　发表于：{{$utils.goodTime(dat.create_at)}}</p>
    <hr />
    <article v-html="dat.content"></article>
    <h3>网友回复：</h3>
    <ul>
      <li v-for="i in dat.replies">
        <p>评论者：{{i.author.loginname}}　　评论于：{{$utils.goodTime(i.create_at)}}</p>
        <article v-html="i.content"></article>
      </li>
    </ul>
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
      id: this.$route.params.id,
      dat: {}
    }
  },
  created () {
    this.loadData()
  },
  methods: {
    loadData () {
      this.$api.get('topic/' + this.id, null, r => {
        this.dat = r.data
      })
    }
  }
}
</script>

<style lang="css">
</style>
