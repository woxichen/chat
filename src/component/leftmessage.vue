<script setup>
const props = defineProps(["message"]);
</script>

<template>
  <!-- 左侧图片 -->
  <a-row>
    <a-col :span="2">
      <img src="/src/assets/maomao.jpg" width="100%" style="padding: 8px" />
    </a-col>
    <a-col :span="20" style="padding: 10px"
      ><div class="messageCard">{{ props.message }}</div></a-col
    >
  </a-row>
</template>

<style scoped>
.messageCard {
  width: fit-content;
  height: 100%;
  background: white;
  border-radius: 8px;
  font-size: 20px;
  padding: 8px;
  position: relative; /* 设置相对定位 */
}

.messageCard::after {
  content: "";
  position: absolute;
  top: 50%;
  left: -15px; /* 调整三角形的水平位置 */
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 5px 0 20px 25px; /* 调整三角形的大小和形状 */
  border-color: transparent transparent transparent white; /* 设置三角形颜色与背景色一致 */
  transform: translateY(-10%) rotate(-280deg); /* 垂直居中三角形 */
}
</style>
