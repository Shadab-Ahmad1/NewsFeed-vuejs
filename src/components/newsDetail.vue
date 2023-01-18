<template>
    <transition name="slide-left">
    <div v-if="sidebarVisible" class="detailModal" >
        <div>
            <button class="close" @click="closeSidebar">hide</button>
        </div>
      <div class="details-container">
      <div class="details-container-img">
        <img :src="article.urlToImage" />
      </div>
      <div class="details-container-title">
        <h4 class="author">By: <span>{{ article.author }}</span></h4>
        <p>{{ new Date(article.publishedAt).toLocaleString('en-US', {year: 'numeric', month: 'long', day: 'numeric', hour: 'numeric', minute: 'numeric'})}}</p>

        <h4 class="title">{{ article.title.slice(0,150)+".." }}</h4>
      </div>
      <div class="details-container-desc">
        <p v-html="article.description.slice(0,400)"></p>
      </div>
      </div>
    </div>
</transition>

  </template>
  

  <script>
export default {
  name: 'newsDetail',
  components: {},
  props: {
    article: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
        sidebarVisible: false,
    };
  },
  methods: {
    closeSidebar() {
      this.sidebarVisible = false;
      this.$emit('close') // Add this line
    }
  },
  mounted() {
  },
  watch: {
    article: function(val) {
      if (val !== null) {
        this.sidebarVisible = true;
      }

    }
  },

};
</script>

<style>
.slide-left-enter-active {
  transition: all .3s ease;
  filter: blur(3px);
}
.slide-left-leave-active {
  transition: all .3s ease;
  filter: blur(0px);

}
.slide-left-enter, .slide-left-leave-to{
  transform: translateX(100%);
  opacity: 0;
}
</style>