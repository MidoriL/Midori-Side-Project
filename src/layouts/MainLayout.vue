<template>
  <q-layout id="mainLayout">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <template v-for="(menuItem, index) in menuList" :key="index">
          <q-item clickable :active="menuItem.label === 'Outbox'" v-ripple @click="goToPage(menuItem.to)">
            <q-item-section avatar>
              <q-icon :name="menuItem.icon" />
            </q-item-section>
            <q-item-section>
              {{ menuItem.label }}
            </q-item-section>
          </q-item>
          <q-separator :key="'sep' + index"  v-if="menuItem.separator" />
        </template>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default({
  name: 'MainLayout',
  components: {
  },
    data () {
    return {
      leftDrawerOpen:true,
      menuList:[
        {
          icon:'home',
          label: 'Home Page',
          to: { name: 'pageIndex' },
        },
        {
          icon:'dashboard',
          label: 'Dashboard',
          to: { name: 'dashboard' },
        }
      ]
    }
    },
    methods:{
      toggleLeftDrawer(){
        this.leftDrawerOpen = !this.leftDrawerOpen
      },
      goToPage(to){
        this.$router.push({ name: to.name })
      }
    }
})
</script>
<style lang="scss">
#mainLayout{
  .q-drawer-container{
    aside{
      width: 200px !important;
    }
  }
}
</style>
