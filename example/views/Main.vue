<!--
 * @Description: 未描述
 * @Author: danielmlc
 * @Date: 2019-08-22 11:35:09
 * @LastEditTime: 2020-02-17 17:28:28
 -->
<template>
  <div class="main">
    <div class="header">
      <div class="logo">
        <img width="50px" src="../asset/img/logo.png"
          alt="logo">
      </div>
      <div class="title">
        element-extension
      </div>
    </div>
    <div class="content">
      <div class="menu">
        <el-scrollbar style="height:100%" wrap-class="pagepanel" view-class="menupanel_view">
          <template v-for="(i,index) in menuData">
            <div v-if="!i.children" :key="index" class="item" @click="goUrl('/' + i.name)">
              {{ i.label }}
            </div>
            <div v-else :key="index">
              <span class="subtitle"> {{ i.label }} </span>
              <div v-for="(ii, iindex) in i.children" :key="iindex" class="item" @click="goUrl('/' + ii.name)">
                {{ ii.label }}
              </div>
            </div>
          </template>
        </el-scrollbar>
      </div>
      <div class="page">
        <el-scrollbar style="height:100%" wrap-class="pagepanel" view-class="pagepanel_view">
          <transition name="fade">
            <router-view />
          </transition>
        </el-scrollbar>
      </div>
    </div>
  </div>
</template>
<script>
  import menuList from './data/menuData.json'
  export default {
    data () {
      return {
        defaultActive: '/base'
      }
    },
    computed: {
      menuData: {
        get () {
          return menuList
        }
      }
    },
    mounted () {
      if (this.$route.path) {
        this.defaultActive = this.$route.path
      } else {
        this.defaultActive = menuList[0].url
      }
    },
    methods: {
      goUrl (url) {
        this.$router.push({
          path: url
        })
      }
    }
  }
</script>

<style lang="postcss" >
  @import  '../../src//styl/var.pcss';
  .main {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction:column;
    & > .header {
      height: 55px;
      line-height:55px;
      background:$primary;
      display: flex;
      padding-left:10px;
      padding-top:5px;
      & > .title {
        height: 100%;
        line-height: 55px;
        color: #fff;
        font-size: 18px;
        font-weight: 600;
        padding-left: 20px;
      }
    }
    & > .content{
      flex:1;
      display: flex;
      overflow: hidden;
      & > .menu{
        height: 100%;
        width: 280px;
        color: $text-regular;
        font-size: 14px;
        & .subtitle {
          color: #aaa;
          font-size: 16px;
        }
        & .item {
          line-height: 45px;
          height: 45px;
          cursor: pointer;
          &:hover {
            color: $primary;
          }
        }
      }
      & > .page {
        height: 100%;
        flex:1;
        overflow: hidden;
        padding: 20px 30px;
        box-sizing: border-box;
      }
    }
  }
  .pagepanel {
    overflow: auto;
  }
  .menupanel_view {
    padding: 10px 20px;
    margin: 0;
    box-sizing: border-box;
  }
  .pagepanel_view {
    padding: 20px;
    margin: 0;
    box-sizing: border-box;
  }
</style>
