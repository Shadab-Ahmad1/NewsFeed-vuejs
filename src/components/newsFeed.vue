<template>
  <div>
    <div v-if="loading" class="loader">
      <div class="loader">
  <div class="lds-ellipsis">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </div>
</div>
</div>
    <div v-else>
    <!-- rest of your template code -->
    <div class="top">
      <div class="inline-circle">
        <div class="circles"></div>
        <div class="circles"></div>
        <div class="circles"></div>
      </div>
    </div>
    <div class="scrollToTop"><a href="#">Scroll To Top</a></div>

    <div class="container">
      <div class="row">
        <div class="column-1">
            <span class="feed">News Feed</span>
          </div>
        <div class="column-2">
          <div class="form-group">
            <input
              type="text"
              v-model="search"
              class="form-control"
              id="search"
              placeholder="Search"
            />
            <button class="form-group-button" @click="getNewsByFilter">search</button>
          </div>
        </div>
        <div class="column-3">
          <div class="select">
            <select v-model="selectedFilter" @change="getNewsByFilter">
              <option class="option" value="today">Today</option>
              <option class="option" value="yesterday">Yesterday</option>
              <option class="option" value="thisWeek">This Week</option>
              <option class="option" value="lastWeek">Last Week</option>
              <option class="option" value="thisMonth">This Month</option>
            </select>
          </div>
        </div>
      </div>
    </div>
    <div class="pro-container">
      <div class="pro" v-for="item in articles" v-bind:key="item.id" @click="getArticleDetails(item)">
        <div class="overlay"></div>
        <img :src="item.urlToImage" />
      <div class="content">
        <h4 class="author">By: <span>{{ item.author ? item.author.slice(0,30) + "..." : "Unknown"}}</span></h4>
        <p>{{item.publishedAt}}</p>
        <h4 class="title">{{ item.title.slice(0,50)+".." }}</h4>
      </div>
      </div>
    </div>
    <keep-alive>
    <newsDetail :article = "selectedArticle" v-if="selectedArticle" @close="toggleVisibility"/>
    </keep-alive>

    <div class="backdrop" :class="{visible: showBackdrop}" @click="toggleVisibility"></div>
    <template v-if="errorMessage">
    <div class="error-message">{{ errorMessage }}</div>
</template>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import jQuery   from 'jquery';
import newsDetail from './newsDetail.vue';

export default {
  name: 'NewsList',
  components: {
    newsDetail
  },

  data() {
    return {
      selectedFilter: "today",
      errorMessage :undefined,
      articles: [],
      search: '',
      selectedArticle: {},
      showSidebar: false,
      deleteClicked: false,
      showBackdrop: false,
      loading: true // added here


    };
  },
  methods: {
    getNewsByFilter() {
      this.loading = true;
      let params;
      if (this.selectedFilter === "today") {
        let today = new Date();
        params = {
          from: today.toISOString().split("T")[0],
          to: today.toISOString().split("T")[0],
        };
      } else if (this.selectedFilter === "yesterday") {
        let yesterday = new Date();
        yesterday.setDate(yesterday.getDate() - 1);

        params = {
          from: yesterday.toISOString().split("T")[0],
          to: yesterday.toISOString().split("T")[0],
        };
      } else if (this.selectedFilter === "thisWeek") {
        let startOfWeek = new Date();
        startOfWeek.setDate(startOfWeek.getDate() - startOfWeek.getDay());
        let endOfWeek = new Date();
        endOfWeek.setDate(endOfWeek.getDate() + (6 - endOfWeek.getDay()));

        params = {
          from: startOfWeek.toISOString().split("T")[0],
          to: endOfWeek.toISOString().split("T")[0],

        };
      } else if (this.selectedFilter === "lastWeek") {
        let startOfWeek = new Date();
        startOfWeek.setDate(
          startOfWeek.getDate() - 7 - (startOfWeek.getDay() - 1)
        );
        let endOfWeek = new Date();
        endOfWeek.setDate(endOfWeek.getDate() - 7 + (7 - endOfWeek.getDay()));

        params = {
          from: startOfWeek.toISOString().split("T")[0],
          to: endOfWeek.toISOString().split("T")[0],

        };
      } else {
        let startOfMonth = new Date();
        startOfMonth.setDate(1);
        let endOfMonth = new Date();
        endOfMonth.setMonth(endOfMonth.getMonth() + 1);
        params = {
          from: startOfMonth.toISOString().split("T")[0],
          to: endOfMonth.toISOString().split("T")[0],

        };
      }
      axios
        .get(
          `https://newsapi.org/v2/everything?q=q=${this.search}&sortBy=popularity&apiKey=f10379a6e77448ee91292012f8eb0934`,
          {
            params,
          }
        )
        .then((response) => {
          this.articles = response.data.articles;
          this.description = response.data.articles.description;
          this.content = response.data.articles.content;
          this.loading = false;
        })
        .catch(error => {
    console.log(error);
    this.errorMessage = "Sorry, there was an error retrieving the news. Please try again later.";
    this.loading = false;
  });
    },
    getArticleDetails(article){
      // console.warn(article);
      this.$nextTick(() => {  
      document.body.style['overflow-y'] = 'hidden';
    }); 
      this.selectedArticle = article;
      this.showBackdrop = true;

    },
    toggleVisibility(){  
    this.showSidebar =false; 
    this.showBackdrop = !this.showBackdrop;         
    this.selectedArticle=false; 
    document.body.style['overflow-y'] = 'auto';
  },
  jQueryMethod() {
    jQuery(window).scroll(function(){
        if (jQuery(this).scrollTop() > 300) {
            jQuery('.scrollToTop').fadeIn();
        } else {
            jQuery('.scrollToTop').fadeOut();
        }
    });
      jQuery('.scrollToTop').click(function(){
        jQuery('html, body').animate({scrollTop : 0},800);
        return false;
    });
  }
  },
  mounted() {
    this.getNewsByFilter();
  }, 
    beforeDestroy() { 
    document.body.style['overflow-y'] = 'auto';
}  
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
.loader {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100%;
}
.lds-ellipsis {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}

.lds-ellipsis div {
  position: absolute;
  top: 27px;
  width: 11px;
  height: 11px;
  border-radius: 50%;
  background: #2586F7;
  animation-timing-function: cubic-bezier(0, 1, 1, 0);
}

.lds-ellipsis div:nth-child(1) {
  left: 6px;
  animation: lds-ellipsis1 0.6s infinite;
}

.lds-ellipsis div:nth-child(2) {
  left: 6px;
  animation: lds-ellipsis2 0.6s infinite;
}

.lds-ellipsis div:nth-child(3) {
  left: 26px;
  animation: lds-ellipsis2 0.6s infinite;
}

.lds-ellipsis div:nth-child(4) {
  left: 45px;
  animation: lds-ellipsis3 0.6s infinite;
}

@keyframes lds-ellipsis1 {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}

@keyframes lds-ellipsis3 {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}

@keyframes lds-ellipsis2 {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(19px, 0);
  }
}

</style>