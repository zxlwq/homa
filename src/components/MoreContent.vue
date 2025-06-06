<template>
  <div class="more-content">
    <div
      contenteditable="true"
      class="editable-text"
      ref="editableDiv"
      @input="updateContent"
    >{{ content }}</div>

    <button @click="saveContent">保存内容</button>
    <p class="hint">刷新页面后内容也会保留</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const content = ref('点击我进行编辑')
const editableDiv = ref(null)

// 页面加载时读取本地存储的内容
onMounted(() => {
  const saved = localStorage.getItem('my-editable-content')
  if (saved) {
    content.value = saved
    if (editableDiv.value) {
      editableDiv.value.innerText = saved
    }
  }
})

// 当用户输入内容时更新 content
function updateContent() {
  content.value = editableDiv.value.innerText
}

// 点击按钮保存到本地
function saveContent() {
  localStorage.setItem('my-editable-content', content.value)
  alert('内容已保存！')
}
</script>

<style scoped>
.more-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
  height: 100vh;
  gap: 12px;
  padding: 16px;
}

.editable-text {
  padding: 12px 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
  min-width: 300px;
  text-align: center;
  font-size: 16px;
  cursor: text;
  outline: none;
  white-space: pre-wrap;
}

.editable-text:focus {
  border-color: #409eff;
  background-color: #f5faff;
}

button {
  padding: 6px 14px;
  background-color: #FFB6C1; /* 樱花粉 */
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background-color: #ff94a8; /* 悬停时深一点的粉 */
}

.hint {
  font-size: 12px;
  color: gray;
}
</style>
