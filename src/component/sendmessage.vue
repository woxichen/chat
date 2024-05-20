<script setup>
import { ref } from "vue";
const emits = defineEmits(["send"]);
const inputValue = ref("");
const handleSend = () => {
  emits("send", inputValue.value);
  inputValue.value = "";
};
const toggleEmojiPicker = ref(false); // 控制表情选择器的显示
const addEmoji = (emoji) => {
  inputValue.value += emoji;
  toggleEmojiPicker.value = false; // 选择表情后关闭表情选择器
};

// 表情数据，您可以根据实际情况从本地存储或其他地方获取
const emojis = [
  { text: "😀" },
  { text: "😂" },
  { text: "👿" },
  { text: "😭" },
  // ...其他表情
];
</script>

<template>
  <a-row>
    <a-col :span="20">
      <a-input
        v-model:value="inputValue"
        placeholder="请输入内容"
        @keyup.enter="handleSend"
        style="background-color: #00e1ffd1; border: 1px solid rgb(0 0 0 / 40%)"
      ></a-input
    ></a-col>
    <a-col :span="1">
      <a-button
        type="default"
        @click="toggleEmojiPicker = !toggleEmojiPicker"
        style="
          width: 100%;
          background-image: url(/src/assets/biaoqing.png);
          background-size: contain;
          margin-left: 10px;
        "
      >
        <SmileOutlined />
      </a-button>
      <!-- 表情选择器弹出层 -->
      <div v-if="toggleEmojiPicker" class="emoji-picker">
        <div v-if="toggleEmojiPicker" class="emoji-picker">
          <img
            v-for="emoji in emojis"
            :alt="emoji.text"
            @click="addEmoji(emoji.text)"
            class="emoji"
          />
        </div>
      </div>
    </a-col>
    <a-col :span="2">
      <a-button
        type="primary"
        @click="handleSend"
        style="
          width: 100%;
          background-image: url(/src/assets/send.png);
          background-size: cover;
          margin-left: 30px;
        "
      ></a-button
    ></a-col>
  </a-row>
</template>

<style scoped>
.emoji-picker {
  position: absolute;
  bottom: 100%;
  top: auto;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 5px;
  box-sizing: border-box; /* 保持原有设置 */
}

.emoji-picker img {
  font-size: 50px; /* 设置表情图片的字体大小 */
  object-fit: cover; /* 使表情图片完全覆盖容器 */
  cursor: pointer;
}
</style>
