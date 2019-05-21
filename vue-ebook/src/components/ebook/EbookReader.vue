<template>
  <div class="ebook-reader">
    <div id="read"></div>
    {{$route.params.fileName}}
  </div>
</template>
<script>
import { mapGetters } from 'vuex'
import Epub from 'epubjs'
global.ePub = Epub
export default {
  computed: {
    ...mapGetters(['fileName'])
  },
  methods: {
    initEpub() {
      const url = 'http://192.168.8.135:8081/epub/' + this.fileName + '.epub'
      this.book = new Epub(url)
      console.log(url, this.book)
    }
  },
  mounted() {
    //const fileName = this.$route.params.fileName.split('|').join('/')
    this.$store
      .dispatch('setFileName', this.$route.params.fileName.split('|').join('/'))
      .then(() => {
        this.initEpub()
      })
    //console.log(fileName)
  }
}
</script>
<style lang="scss" scoped>
@import '../../assets/styles/global.scss';
</style>
