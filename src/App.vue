<template>
  <v-app>
    
    <v-navigation-drawer app clipped floating width="240">
      <content-placeholders class="mt-3" v-if="loading">
        <content-placeholders-text :lines="1" />
      </content-placeholders>
      <v-btn v-else color="primary btn__add__menu" :to="'/danh-sach-ho-so/' + currentIndex + '/tiep-nhan-ho-so'">
        <v-icon>add_circle</v-icon>
        Thêm hồ sơ tiếp nhận
      </v-btn>
      <content-placeholders class="mt-3" v-if="loading">
        <content-placeholders-text :lines="7" />
        </content-placeholders>
      <v-list v-else class="py-0 nav_trang_thai_ho_so">
        <v-list-tile v-for="(item, index) in trangThaiHoSoList" :key="item.id" :to="'/danh-sach-ho-so/' + index">
          <v-list-tile-action>
            <v-icon>{{item.action}}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    
    <v-content>
      <router-view></router-view>
    </v-content>
    
  </v-app>
</template>

<script>
  export default {
    data: () => ({}),
    computed: {
      loading () {
        return this.$store.getters.loading
      },
      currentIndex () {
        return this.$store.getters.index
      },
      trangThaiHoSoList () {
        return this.$store.getters.loadtrangThaiHoSoList
      }
    },
    created () {
      var vm = this
      vm.$nextTick(function () {
        vm.$store.dispatch('loadtrangThaiHoSoList')
      })
    }
  }
</script>

<style lang="stylus">
  @import './stylus/main'
</style>
