<template>
  <div class="personlist-container">
    <div class="items">
      <div class="item" v-for="item in personlist" :key="item.id" @click="toplaylist(item.id)">
        <img :src="item.coverImgUrl" alt="">
        <div class="info">
          <span class="playlistname">{{ item.name }}</span>
          <span class="playcount">{{ item.playCount }}</span>
          <span class="trackcount">总数:{{ item.trackCount }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      personlist: []
    }
  },
  async created () {
    const { data: resfour } = await this.$axios.get('/api/login/status')
    if (resfour.data.profile !== null && resfour.data.account !== null) {
      this.$api.getPersonMusicList(resfour.data.profile.userId).then(val => {
        this.personlist = val
      })
    }
  },
  methods: {
    toplaylist (id) {
      this.$router.push(`/home/playlist?q=${id}`)
    }
  }
}
</script>

<style>
</style>
