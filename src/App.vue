<script setup lang="ts">
import { ref } from 'vue'

const xiaohongshuText = ref('');
const urls = ref<string[]>([]);

const extractUrlsFromText = () => {
    const urlRegex = /https?:\/\/[^\s,，]+/g;
    urls.value = xiaohongshuText.value.match(urlRegex) || [];

    if (urls.value.length > 0) {
      // 打开所有提取到的链接（新窗口）
      urls.value.forEach(url => {
        window.open(url, '_blank');
      });
    } else {
      alert('未提取到有效的URL');
    }
  };
</script>

<template>
  <div class="container">
    <h1>提取链接</h1>
    <div class="input-group">
      <textarea 
        v-model="xiaohongshuText" 
        placeholder="粘贴文本内容，并提取其中的链接..." 
        rows="4"
        class="textarea"
      ></textarea>
    </div>
    <div class="input-group">
      <button @click="extractUrlsFromText" class="btn">提取链接</button>
    </div>
    <div v-if="urls.length" class="result">
      <h3>提取到的链接：</h3>
      <ul>
        <li v-for="(url, index) in urls" :key="index">{{ url }}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
/* 基础样式重置 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* 页面容器 - 实现垂直水平居中 */
body {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f5f7f5;
}

/* 主容器样式 */
.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
}

/* 标题样式 */
h1 {
  color: #27ae60;
  font-size: 2rem;
  margin-bottom: 1rem;
  text-align: center;
}

/* 输入区域样式 */
.textarea {
  width: 100%;
  padding: 1rem;
  border: 2px solid #2ecc71;
  border-radius: 6px;
  font-size: 1rem;
  min-height: 120px;
  resize: vertical;
  transition: all 0.3s ease;
  background-color: #ffffff;
}

.textarea:focus {
  outline: none;
  border-color: #27ae60;
  box-shadow: 0 0 0 3px rgba(46, 125, 50, 0.1);
}

/* 按钮样式 */
.btn {
  width: 100%;
  padding: 0.8rem 1.5rem;
  background-color: #27ae60;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 500;
}

.btn:hover {
  background-color: #219653;
  transform: translateY(-2px);
}

/* 结果区域样式 */
.result {
  width: 100%;
  margin-top: 1.5rem;
  padding: 1rem;
  border-radius: 6px;
  background-color: #f5f5f5;
}

.result h3 {
  color: #2e7d32;
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
}

.result ul {
  list-style: none;
  padding: 0;
}

.result li {
  margin: 0.5rem 0;
  padding: 0.5rem;
  background-color: #ffffff;
  border-radius: 4px;
  word-break: break-all;
}

.input-group {
  width: 100%;
}
</style>
