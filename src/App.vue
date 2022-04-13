<template>
  <div id="app">
    <div class="whole-container">
      <sidebar-component
        @width="setWidth"
      />
      <div class="content-component">
        <header-component />
        <ContentComponent />
        <FooterComponent />
      </div>
    </div>
  </div>
</template>

<script>
  import SidebarComponent from "./components/SidebarComponent.vue";
  import HeaderComponent from "./components/HeaderComponent";
  import ContentComponent from "./components/ContentComponent";
  import FooterComponent from "./components/FooterComponent";
export default {
  name: 'app',
  components: {
    FooterComponent,
    ContentComponent,
    HeaderComponent,
    SidebarComponent
  },
  data () {
    return {
      collapsed: false
    }
  },
  methods: {
    setWidth(val) {
      console.log(val);
      this.collapsed = val;
      if(this.collapsed == false){
        $('.content-component').removeClass('width-100-85');
      }
      else{
        $('.content-component').addClass('width-100-85');
      }
    }
  },

}
</script>

<style>
  .whole-container{
    width: 100%;
    display: inline-flex;
    align-items: flex-start;
    overflow: hidden;
  }
  .content-component{
    width: calc(100% - 230px);
    height: 100%;
  }
  .width-100-85{
    width: calc(100% - 85px);
  }
  .width-100-85 .footer{
    width: calc(100% - 85px) !important;
  }
</style>
