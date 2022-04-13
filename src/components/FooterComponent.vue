<template>
<div class="footer">
  <div class="d-flex align-items-center justify-content-start">
    <p class="mr-3 mb-0 text">Privacy Policy</p>
    <div class="border"></div>
    <p class="ml-3 mb-0 text">Terms of use</p>
  </div>
  <p class="text mb-0">Copyright @ 2022 Soho House All rights reserved</p>
</div>
</template>

<script>
    export default {
        name: "FooterComponent"
    }
</script>

<style scoped>
  .footer{
    padding: 15px 10px;
    border-top: 1px solid #dedede;
    width: calc(100% - 230px);
    position: absolute;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #edf1f4;
  }
  .border {
    width: 1px;
    background: #162b43;
    height: 25px;
  }
.text{
  color: #666666;
  font-size: 11px;
}
</style>
