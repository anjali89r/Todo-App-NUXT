<template>
   <header id="header">

      <div class="main-menu">
        <v-navigation-drawer class="sideDrawer" v-model="sideNav" fixed temporary dark>
          <v-list-tile>
            <v-list-tile-action>
              <v-icon>home</v-icon>
            </v-list-tile-action>
            <v-list-tile-title>
              <nuxt-link to="/">Home</nuxt-link>
            </v-list-tile-title>
          </v-list-tile>


          <v-list-tile>
            <v-list-tile-action></v-list-tile-action>
            <v-list-tile-title>
              <router-link to="/completed">All Complete</router-link>
            </v-list-tile-title>
          </v-list-tile>
        </v-navigation-drawer>
        <v-toolbar class="main-toolbar">
          <v-toolbar-side-icon @click.native.stop="sideNav=!sideNav" class="hidden-md-and-up"></v-toolbar-side-icon>


          <v-spacer></v-spacer>
          <v-toolbar-items class="hidden-sm-and-down">
            <v-btn flat>
              <nuxt-link to="/">Home</nuxt-link>
            </v-btn>


            <v-btn flat>
              <nuxt-link to="/completed">All Complete</nuxt-link>
            </v-btn>

          </v-toolbar-items>
        </v-toolbar>
      </div>
    </header>
</template>
<script>
export default {
  name: "Nav",

  data: () => ({
    products: [
      { title: "Dhoti", to: "dhoti", icon: "people_outline" },
      { title: "Set Saree", to: "kerala-saree", icon: "people_outline" },
      { title: "Set Mundu", to: "set-mundu", icon: "people_outline" }
      // { title: "Salwar", to: "salwar" }
    ],
    sideNav: null
    // items: [
    //   { title: "Home", icon: "dashboard", to: "/" },
    //   { title: "Products", icon: "dashboard", to: "#" },
    //   { title: "Blog", icon: "dashboard", to: "/blog" },
    //   { title: "Contact", icon: "question_answer" }
    // ]
  }),
  components: {
    Footer
  }
};
</script>
<style scoped>
#header {
  transition: all 0.5s;
  z-index: 997;
  background: #fff;
}
.v-list__group__header--active .v-list__group__header__prepend-icon .v-icon {
  color: #fff;
}
.main-menu .main-toolbar {
  background-color: #000;
}
.main-menu .main-toolbar .v-toolbar__title,
.main-menu .main-toolbar .v-toolbar__items .v-btn {
  font-size: 13px;
}
.main-menu .main-toolbar .v-toolbar__items .v-btn:hover,
.v-btn a:hover {
  color: #90d3f0;
}
.v-menu__content {
  top: 64px !important;
}
.menu-list .v-list__tile a {
  font-size: 13px;
  color: #ed620c;
  text-decoration: none;
}
.menu-list .v-list__tile a:hover {
  color: #914414;
}
.menu-list .v-list__tile {
  height: 35px !important;
}
.main-vmenu .v-btn {
  background-color: #000 !important;
}
a {
  font-size: 13px;
  color: #e48a17;
  text-decoration: none;
  font-weight: 800;
}
#header {
  position: fixed;
  width: 100%;
}
.content-sec {
  padding-top: 110px !important;
}
.v-navigation-drawer {
  margin-top: 110px !important;
  height: 200% !important;
  max-height: calc(200% - 0px) !important;
}
</style>
