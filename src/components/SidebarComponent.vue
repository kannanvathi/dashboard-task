<template>
  <div class="row" id="body-row">
    <div id="sidebar-container" class="sidebar-expanded d-none d-md-block">
      <div class="large-logo">
        <img src="src/assets/images/soho_house_logo.png" width="80">

      </div>
      <div class="small-logo d-none">
        <img src="src/assets/images/soho-logo.png" width="40">
      </div>
      <a href="#" data-toggle="sidebar-colapse" @click="toggleImage()" class="bg-dark list-group-item list-group-item-action d-flex align-items-center p-0">
        <div class="d-flex w-100 justify-content-start align-items-center">
          <span id="collapse-text"><i class="fa-solid fa-angle-right"></i></span>
        </div>
      </a>
      <ul class="list-group">
        <li class="pl-3 pr-3 pb-2 pt-3">
        <a href="#" class="list-group-item bg-dark dashboard active" v-on:click="activeTab('dashboard')">
          <i class="fa-solid fa-bars mr-3"></i>
          <span class="menu-collapsed">Dashboard</span>
        </a>
        </li>
        <li class="pl-3 pr-3">
          <a href="#" class="list-group-item search bg-dark" v-on:click="activeTab('search')">
            <i class="fa-solid fa-magnifying-glass mr-3"></i>
            <span class="menu-collapsed">Search</span>
          </a>
        </li>

        <!--<a href="#submenu1" data-toggle="collapse" aria-expanded="false" class="bg-dark list-group-item list-group-item-action flex-column align-items-start">
          <div class="d-flex w-100 justify-content-start align-items-center">
            <span class="fa fa-dashboard fa-fw mr-3"></span>
            <span class="menu-collapsed">Dashboard</span>
            <span class="submenu-icon ml-auto"></span>
          </div>
        </a>
        <div id='submenu1' class="collapse sidebar-submenu">
          <a href="#" class="list-group-item list-group-item-action bg-dark">
            <span class="menu-collapsed">Charts</span>
          </a>
          <a href="#" class="list-group-item list-group-item-action bg-dark">
            <span class="menu-collapsed">Reports</span>
          </a>
          <a href="#" class="list-group-item list-group-item-action bg-dark">
            <span class="menu-collapsed">Tables</span>
          </a>
        </div>-->
      </ul>
    </div>
  </div>
</template>

<script>
    export default {
        name: "SidebarComponent",
      data() {
          return {
            collapsed: false,
          }
      },
      mounted() {
        $(document).ready(function(){
          // Hide submenus
          $('#body-row .collapse').collapse('hide');

          // Collapse/Expand icon
          $('#collapse-icon').addClass('fa-angle-double-left');

          // Collapse click
          $('[data-toggle=sidebar-colapse]').click(function() {
            SidebarCollapse();
          });

          function SidebarCollapse () {
            $('.menu-collapsed').toggleClass('d-none');
            $('.sidebar-submenu').toggleClass('d-none');
            $('.submenu-icon').toggleClass('d-none');
            $('#sidebar-container').toggleClass('sidebar-expanded sidebar-collapsed');

            // Collapse/Expand icon
            $('#collapse-icon').toggleClass('fa-angle-double-left fa-angle-double-right');
          }
        });
      },
      methods: {
        activeTab(item){
          $('.list-group-item').removeClass('active');
          if(item == 'dashboard'){
            $('.search').removeClass('active');
            $('.dashboard').addClass('active');
          }
          else{
            $('.dashboard').removeClass('active');
            $('.search').addClass('active');
          }
        },
        toggleImage(){
          if($('#sidebar-container').hasClass('sidebar-collapsed')){
            $('.small-logo').addClass('d-none');
            $('.large-logo').removeClass('d-none');
            $('.fa-angle-right').removeClass('rotate');
            this.collapsed = false;
          }
          else{
            $('.large-logo').addClass('d-none');
            $('.small-logo').removeClass('d-none');
            $('.fa-angle-right').addClass('rotate');
            this.collapsed = true;
          }
          this.$emit('width', this.collapsed);
        }
      },
    }
</script>

<style scoped>
  #body-row {
    margin-left:0;
    margin-right:0;
    height: 100%;
  }
  #sidebar-container {
    min-height: 100vh;
    background-color: #fff;
    padding: 0;
    height: 100%;
  }

  /* Sidebar sizes when expanded and expanded */
  .sidebar-expanded {
    width: 230px;
  }
  .sidebar-collapsed {
    width: 85px;
  }

  /* Menu item*/
  #sidebar-container .list-group a {
    height: 35px;
    font-size: 12px;
    color: #162b43;
    padding: 0 15px;
    border: none;
  }

  /* Submenu item*/
  #sidebar-container .list-group .sidebar-submenu a {
    height: 45px;
    padding-left: 30px;
  }
  .sidebar-submenu {
    font-size: 0.9rem;
  }

  /* Separators */
  .sidebar-separator-title {
    background-color: #fff;
    height: 55px;
    border: none;
  }
  .sidebar-separator {
    background-color: #333;
    height: 25px;
  }
  .logo-separator {
    background-color: #333;
    height: 60px;
  }

  /* Closed submenu icon */
  #sidebar-container .list-group .list-group-item[aria-expanded="false"] .submenu-icon::after {
    content: " \f0d7";
    font-family: FontAwesome;
    display: inline;
    text-align: right;
    padding-left: 10px;
  }
  /* Opened submenu icon */
  #sidebar-container .list-group .list-group-item[aria-expanded="true"] .submenu-icon::after {
    content: " \f0da";
    font-family: FontAwesome;
    display: inline;
    text-align: right;
    padding-left: 10px;
  }
  #collapse-text{
    position: absolute;
    right: -16px;
    background: #162b43;
    width: 30px;
    height: 30px;
    display: inline-flex;
    color: #fff;
    align-items: center;
    justify-content: center;
    top: 55px;
    border-radius: 50%;
    z-index: 1;
  }
  .list-group-item.active{
    background-color: #162b43 !important;
    color: #fff !important;
  }
  .small-logo, .large-logo{
    text-align: center;
    padding: 15px;
  }
  .rotate{
    transform: rotate(180deg);
  }
</style>
