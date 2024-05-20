<script setup>
import { ref } from "vue";
import leftmessage from "./component/leftmessage.vue";
import Rightmessage from "./component/Rightmessage.vue";
import sendmessage from "./component/sendmessage.vue";
import Header from "./component/Header.vue";
import axios from "axios";
const messageList = ref([]);
const handleSend = async (value) => {
  messageList.value.push({
    position: "right",
    message: value,
  });
  // 对应的百度云api
  // 用map
  const messages = messageList.value.map((item) => {
    return {
      role: item.position == "left" ? "assistant" : "user",
      content: item.message,
    };
  });
  // axios请求分get(传params）和post（传ID）,处理返回数据需要加await转同步，在async中使用
  const res = await axios.request({
    url: "",
    method: "POST",
    data: {
      messages,
      system: "",
    },
  });
  messageList.value.push({
    position: "left",
    message: res.data.result,
  });
};
</script>
<template>
  <div class="container" style="height: 100%">
    <Header></Header>
    <div
      style="
        overflow: scroll;
        height: calc(100vh - 50px - 40px);
        scrollbar-width: none;
      "
    >
      <!-- 消息展示 -->
      <div v-for="(item, index) in messageList" :key="index">
        <leftmessage
          v-if="item.position == 'left'"
          :message="item.message"
        ></leftmessage>
        <Rightmessage
          v-if="item.position == 'right'"
          :message="item.message"
        ></Rightmessage>
      </div>
    </div>
    <!-- 发送消息 -->
    <sendmessage
      style="position: absolute; bottom: 0px; width: 100%"
      @send="handleSend"
    ></sendmessage>
  </div>
</template>

<style scoped>
.container {
  width: 50%;
  position: absolute;
  left: 50%;
  transform: translate(-50%);
  background-image: url(./assets/background.png);
  height: 100%;
}
@media only screen and (max-width: 600px) {
  .container {
    width: 90%; /* 或者设置为 100% 以填充整个屏幕宽度 */
  }
}

/* 对于中等大小的设备，例如平板 */
@media only screen and (min-width: 601px) and (max-width: 1024px) {
  .container {
    width: 80%;
  }
}

/* 对于较大的屏幕，例如桌面 */
@media only screen and (min-width: 1025px) {
  .container {
    width: 50%;
  }
}
</style>
