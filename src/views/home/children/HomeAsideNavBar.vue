<template>
  <div class="asidenav">
    <el-menu
      router
      active-text-color="red"
      default-active="/home/individuation"
    >
      <el-menu-item
        :index="item.path"
        :key="index"
        v-for="(item, index) in navMenu"
      >
        <template slot="title">
          <i class="iconfont" :class="item.icon"></i>
          <span class="song_">{{ item.menu }}</span>
        </template>
      </el-menu-item>
    </el-menu>

    <el-menu active-text-color="black" unique-opened>
      <el-submenu index="1">
        <template slot="title">
          <i class="iconfont icon-diqiu"></i>
          <span class="song_">创建的歌单</span>
        </template>
        <el-menu-item
          @click="songListClick(item)"
          v-for="(item, index) in myList"
          :key="index"
        >
          <i class="iconfont icon-yinyue"></i> {{ item.name }}
        </el-menu-item>
      </el-submenu>

      <el-submenu index="2">
        <template slot="title">
          <i class="iconfont icon-diqiu"></i
          ><span class="song_">收藏的歌单</span>
        </template>
        <el-menu-item
          @click="songListClick(item)"
          v-for="(item, index) in subList"
          :key="index"
        >
          <i class="iconfont icon-yinyue"></i> {{ item.name }}
        </el-menu-item>
      </el-submenu>
    </el-menu>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'HomeAsideNavBar',
  data() {
    return {
      navMenu: [
        {
          menu: '个性推荐',
          path: '/home/individuation',
          icon: 'icon-airec-zhinengtuijian'
        },
        { menu: '歌单推荐', path: '/home/playlist', icon: 'icon-yinyue' },
        { menu: '最新音乐', path: '/home/songs', icon: 'icon-yinyue' },
        { menu: '最新mv', path: '/home/mv', icon: 'icon-MV' },
        { menu: '排行榜', path: '/home/leaderboard', icon: 'icon-yinyue' },
        { menu: '歌手', path: '/home/singer', icon: 'icon-geshou' }
      ],
      myList: [],
      subList: []
    }
  },
  methods: {
    songListClick(item) {
      window.sessionStorage.setItem('id', item.id)
      this.$bus.$emit('newDetail', item.id)
      this.$router.push(`/home/detail/${item.id}`)
    }
  },
  computed: {
    ...mapState(['userInfo'])
  },
  watch: {
    userInfo: {
      handler(n, o) {
        this.myList = n.myList
        this.subList = n.subList
      }
    }
  }
}
</script>

<style scoped>
.el-menu-item {
  font-size: 13px;
}
.song_ {
  font-size: 12px !important;
  margin-left: 10px;
}
.author {
  width: 100%;
}
.img {
  position: absolute;
  bottom: 100px;
  width: 200px;
}
.img div {
  padding: 10px;
}
img {
  width: 100%;
}
</style>
