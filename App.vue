<template>
  <view class="container">
    <Content></Content>
  </view>
</template>

<script>
import axios from 'axios';
import Content from './components/Content';
 
export default {
  components:{
    Content,
  },

}
</script>

<style>
.container {
  background-color: #3e46b4;
  flex: 1;
  flex-direction: column;
}
</style>


