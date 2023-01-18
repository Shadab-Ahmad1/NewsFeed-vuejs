<template>
  <div id="app">
    <newsFeed />
  </div>
</template>

<script>
import newsFeed from './components/newsFeed.vue';
export default {
  name: 'App',
  components: {
    newsFeed,
  },
  data(){
    return {
      posts:undefined
    }
  },
  methods:{
    filterNews () {


    }
  }
}
</script>

<style>
body{
  margin: 0;
  padding: 0;
  overflow-x: hidden;

}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #F5F5F5;

}
.error-message{
    position: absolute;
    background: #c51244;
    color: #fff;
    padding: 10px 0;
    right: 12%;
    width: 79%;
    text-align: center;
    margin: 0 auto;
    top: 53%;
}
.pro-container{
    display: flex;
    justify-content: space-between;
    padding-top: 20px;
    max-width: 90%;
    margin: 0 auto;
    flex-wrap: wrap;
}
.pro-container .pro{
    width: 32%;
    position: relative;
    cursor: pointer;
    border: 1px solid #cce7d0;
    border-radius: 8px;
    background-color: #fff;
    box-shadow: 20px 20px 30px rgb(0 0 0 / 2%);
    margin-bottom: 30px;
}
.pro-container .pro img{
  width: 100%;
  height: 344px;
  border-radius: 8px;
  margin-top: -1px;
}
.overlay {
    position: absolute;
    z-index: 1;
    border-radius: 8px;
    width: 100%;
    height: 100%;
    background: linear-gradient(180deg, rgba(38, 47, 50, 0) 0%, #262F32 70.94%);
}
.overlay:hover{
  background: linear-gradient(180deg, rgba(38, 47, 50, 0) 0%, #5e5e5e 70.94%);
  transition: all 0.3s ease;

}
.pro .content{
    margin-top: -115px;
    z-index: 1;
    position: absolute;
    max-width: 100%;
}
.pro-container .pro span,
.author span{
    color:#2586F7;
    font-weight: 600;
}
.pro-container .pro p,
.details-container-title .author p{
    font-size: 14px;
    margin-top: 5px;
    margin-bottom: 8px;
    color: #F4F4F4;
    padding-left: 15px;
}
.pro-container .pro .title,
.pro-container .pro .author{
  font-size: 16px;
  margin-top: 2px;
  padding-left: 15px;
  font-weight: 100;
  margin-bottom: 0;
  width: 85%;
  color: #fff;
}
.pro-container .pro .title{
  font-size: 20px;
  font-weight: 600;
}
.container {
    max-width: 90%;
    margin: 0 auto;
}
.row{
    display: flex;
    padding-top: 20px;
    width: 100%;
    align-items: center;
    justify-content: space-between;
}
.column-1{
  width: 13%;
  position: relative;
}
.column-2{
  width: 77%;
}
.column-2 .form-group{
  display: flex;
  align-items: center;
}
.column-3{
  width: 10%;
}
.select{
  text-align: right;
}
.feed{
  font-size: 27px;
  color: #000;
  padding-right: 50px;
}
.feed::after{
  content: '';
    width: 2px;
    height: 47px;
    background-color: #D6DAE4;
    position: absolute;
    top: -6px;
    right: 40px;
}
.form-group .form-control{
    width: 490px;
    padding: 12px;
    outline: none;
    background: #FFFFFF;
    border: 1px solid #EFF0F6;
    border-radius: 12px;
}
.select select {
    padding: 13px 53px 13px 14px;
    background: #FFFFFF;
    border: 1px solid #EFF0F6;
    appearance: none;
    border-radius: 12px;
    background-position: 90% 48%;
    background-image: url('assets/Chevron-Left.png');
    background-repeat: no-repeat;
    outline: none;
    
}
.form-group .form-group-button{
    padding: 19px 20px;
    border-radius: 12px;
    border: none;
    outline: none;
    margin-left: -45px;
    background-image: url('assets/Vector-2.png');
    font-size: 0;
    background-color: #fff;
    background-repeat: no-repeat;
    background-position: center;
    cursor: pointer;
}
.top{
    background-color: black;
    height: 35px;

}
.inline-circle{
    display: flex;
    padding-top: 10px;
    padding-left: 11px;
}
.circles{
    background-color: #fff;
    height: 11px;
    width: 11px;
    margin-right: 4px;
    border-radius: 50%;
}
.scrollToTop {
    position: fixed;
    bottom: 20px;
    right: 20px;
    font-size: 0;
    background: #fff;
    background-image: url('assets/Chevron-Left.png');
    padding: 20px 20px;
    text-align: center;
    background-repeat: no-repeat;
    text-decoration: none;
    border-radius: 8px;
    background-position: center;
    transform: rotate(180deg);
    cursor: pointer;
}

.detailModal{
    position: fixed;
    top: 0;
    right: 0%;
    width: 550px;
    overflow-y: scroll;
    background-color: #fff;
    height: 100%;
    z-index: 2;
}
.details-container{
  padding: 70px 20px;
}
.details-container-img img{
    width: 505px;
    height: 340px;
    border-radius: 10px;
}
.close{
    position: absolute;
    background-image: url('assets/Close.png');
    right: 10px;
    font-size: 0;
    cursor: pointer;
    padding: 13px 11px;
    border: none;
    outline: none;
    background-color: #fff;
    background-repeat: no-repeat;
    background-size: 23px;
    top: 23px;

}
.backdrop{
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  visibility: hidden;
  transition: all 0.1s ease;
}
.backdrop.visible{
  visibility: visible;
  transition: all 0.3s ease;
}

@media only screen and (max-width: 1666px){

/* .form-group .form-group-button {
    padding: 18px 20px;
    right: 52%;
    top: 58px;
} */
.feed::after {
  right: 26px;
}
}
@media only screen and (max-width: 1600px){
  .feed {
    padding-right: 30px;
}

}
@media only screen and (max-width: 1496px){

.pro-container .pro .title{
  font-size: 17px;
}
/* .form-group .form-group-button{
  right: 49%;
    top: 58px;
} */
.feed {
  padding-right: 10px;
}
.feed::after {
  right: 20px;
}
}
@media only screen and (max-width: 1400px){
  .feed::after {
  right: 12px;
}
}
@media only screen and (max-width: 1360px){

/* .form-group .form-group-button {
  right: 45%;
    top: 58px;
} */
.feed {
    padding-right: 10px;
}
.feed::after {
    right: 8px;
}
}
@media only screen and (max-width: 1280px){
  .feed {
    padding-right: 5px;
}
.feed::after {
    right: 3px;
}
}
@media (max-width: 850px){
  body{
  overflow-x: hidden;

}
  .pro-container .pro {
    width: 48%;
  }
  .row {
    flex-direction: column;
}
.column-1 {
    width: 100%;
    text-align: center;
}
.column-2 {
    width: 70%;
    position: relative;
    bottom: -44px;
    left: -15%;
}
.column-3 {
    width: 30%;
    position: relative;
    left: 35%;
}
.form-group .form-control {
    width: 332px;

}
.feed::after{
  display: none;
}
.detailModal {
    right: 0%;
    width: 450px;

}
.details-container-img img {
    width: 100%;
    height: 287px;

}
}
@media (max-width: 477px){
  .pro-container .pro {
    width: 100%;
  }
  .detailModal {
    right: 0%;
    width: 400px;
}
.details-container-img img {
    width: 100%;
    height: auto;
}
.column-1 {
    margin-bottom: 20px;
}
.column-2 {
    width: 100%;
    margin-bottom: 30px;
    position: initial;
}
.column-3 {
    width: 100%;
    position: initial;
}
.close {
    right: 19px;
}
}
</style>


