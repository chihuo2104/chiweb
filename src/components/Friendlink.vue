<template>
  <div id="friendlink">
    <Card class="scroll">
      <h1>{{$t('friendlink')}}</h1>
      <div v-for="i in links" :key="i.name">
        <a :href="i.site" target="_blank" :key="i.site" :title="i.describe">{{i.name}}</a><br>
      </div>
      <p>{{$t('moeicp')}}</p>
      <p>{{$t('zwf')}}</p>
    </Card>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  mounted () {
    axios
      .get('https://cdn.jsdelivr.net/gh/chihuo2104/friends/friends/index.json')
      .then(response => {
        // console.log(response)
        if (this.$store.state.development) { console.log(response.data) }
        this.info = response.data
        if (this.$store.state.development) { console.log(response.info) }
      })
      .then(() => {
        if (this.$store.state.development) { console.log(this.info) }
        this.info.forEach(element => {
          if (this.$store.state.development) { console.log(this.links) }
          if (this.$store.state.development) { console.log(element) }
          axios
            .get('https://cdn.jsdelivr.net/gh/chihuo2104/friends/friends/' + element)
            .then(response => (this.links.push(response.data)))
          if (this.$store.state.development) { console.log(this.links) }
        })
      })
      .then(() => {
        if (this.$store.state.development) { console.log(this.links) }
      })
  },
  data () {
    return {
      info: [],
      links: [],
      index: 1
    }
  }
}
</script>
<style>
</style>
