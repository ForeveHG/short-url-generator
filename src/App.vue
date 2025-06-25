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
        placeholder="粘贴小红书分享的文本" 
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
.container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 0 1rem;
  text-align: center;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 16px;
  justify-content: center;
  margin-top: 20px;
}

.textarea {
  width: 100%;
}

.btn {
  width: 100%;
  padding: 12px 24px;
}

.btn {
  width: 100%;
  padding: 8px 16px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #359469;
}

.textarea {
  width: 100%;
  margin: 0 16px;
  padding: 0.8rem;
  border: 1px solid #4CAF50;
  border-radius: 4px;
  font-size: 1rem;
  min-height: 100px;
  resize: vertical;
  background-color: #f9f9f9;
  transition: all 0.3s ease;
  box-shadow: none;
}

.textarea:focus {
  outline: none;
  border-color: #2E7D32;
  box-shadow: 0 0 0 2px rgba(76, 175, 80, 0.2);
  background-color: #ffffff;
}
</style>
