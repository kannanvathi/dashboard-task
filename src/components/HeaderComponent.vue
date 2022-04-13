<template>
  <div class="header">
  <p class="">Dashboard</p>
  <div class="right-content">
    <div class="dropdown mr-3">
      <a class="dropdown-toggle notification mr-3" type="button" id="menu1" data-toggle="dropdown">
        <i class="fa-solid fa-bell"></i>
        <span class="count">4</span>
      </a>
      <ul class="dropdown-menu" role="menu" aria-labelledby="menu1">
        <li role="presentation"><a role="menuitem" tabindex="-1" href="#" style="font-size: 16px;">Notifications</a></li>
        <li role="presentation" class="divider"></li>
        <li role="presentation" class="mb-2"><a role="menuitem" tabindex="-1" href="#">Something else</a></li>
        <li role="presentation"><a role="menuitem" tabindex="-1" href="#">Lorem ipsum</a></li>
      </ul>
    </div>
    <div class="profile mr-3">
      <div class="img-box">
        <img src="src/assets/images/avatar.png" width="30">
      </div>
      <div class="">
        <p class="profile-name mb-0">Bharathi</p>
        <p class="designation mb-0">Front End Developer</p>
      </div>
    </div>
    <div class="logout mr-3">
      <i class="fa-solid fa-right-from-bracket"></i>
    </div>
  </div>

  </div>
</template>

<script>
    export default {
        name: "HeaderComponent"
    }
</script>

<style scoped>

  .header{
    height: 70px;
    background-color: #fff;
    display: inline-flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
  }
  .header p{
    font-size: 13px;
    color: #162b43;
  }
  .right-content{
    display: inline-flex;
    align-items: center;
    justify-content: flex-start;
  }
  .profile{
    display: inline-flex;
    align-items: center;
    justify-content: center;
  }
  .profile .img-box{
    width: 30px;
    height: 30px;
    background-repeat: no-repeat;
    background-position: center;
    margin-right: 10px;
  }
  .profile-name{
    font-size: 13px;
    color: #162b43;
  }
  .header p.designation{
    font-size: 11px;
    color: #666;
    font-weight: normal;
  }

  /*dropdown css start*/
  .dropdown-menu{
    left: -116px !important;
    top: 10px !important;
    border: 1px solid rgba(0,0,0,.05) !important;
    padding: 10px;
    font-size: 12px;
    color: #162b43;
  }
  .dropdown-menu:before {
    position: absolute;
    top: -7px;
    left: 115px;
    display: inline-block;
    border-right: 7px solid transparent;
    border-bottom: 7px solid #ccc;
    border-left: 7px solid transparent;
    border-bottom-color: rgba(0, 0, 0, 0.2);
    content: '';
  }
  .dropdown-menu.pull-right:before {
    right: 9px;
    left: auto;
  }

  .dropdown-menu:after {
    position: absolute;
    top: -6px;
    left: 116px;
    display: inline-block;
    border-right: 6px solid transparent;
    border-bottom: 6px solid #ffffff;
    border-left: 6px solid transparent;
    content: '';
  }
  .dropdown-menu.pull-right:after {
    right: 10px;
    left: auto;
  }
  .dropdown-menu a{
    padding: 10px 5px !important;
    color: #162b43 !important;
    text-decoration: none !important;
  }
  .dropdown-menu .divider{
    padding: 10px;
    border-bottom: 1px solid #aaa;
    position: relative;
    top: -10px;
  }
  .count{
    font-size: 10px;
    position: absolute;
    background: red;
    width: 15px;
    height: 15px;
    border-radius: 50%;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    left: 10px;
    top: -5px;
  }
  .dropdown-toggle::after{
    display: none !important;
  }
  .header > p {
    color: #162b43;
    margin-bottom: 0;
    font-size: 18px;
    padding-left: 20px;
  }
</style>
