<template>
<div class="login-container">
  <!-- 切换标签 -->
    <div class="tabs">
      <span class="tab active" data-tab="password">账号登录</span>
      <span class="tab" data-tab="sms">手机验证码</span>
    </div>

  <!-- 内容区域 -->
  <div class="tab-content">
    <!-- 账号密码登录 -->
    <div class="tab-pane" id="password">
      <input type="text" placeholder="用户名">
      <input type="password" placeholder="密码">
      <button>登录</button>
    </div>

    <!-- 手机验证码登录 -->
    <div class="tab-pane" id="sms">
      <input type="tel" placeholder="手机号">
      <div style="display: flex; gap: 10px;">
        <input type="text" placeholder="验证码">
        <button style="flex: 1;">获取验证码</button>
      </div>
      <button>登录</button>
    </div>
  </div>
</div>
</template>

<script setup>
  // 获取所有标签和内容
  const tabs = document.querySelectorAll('.tab');
  
  tabs.forEach(tab => {
    tab.addEventListener('click', () => {
      const target = tab.dataset.tab; // 获取目标 id

      // 清除所有 active
      document.querySelector('.tab.active').classList.remove('active');
      document.querySelector('.tab-pane.active').classList.remove('active');

      // 设置当前为 active
      tab.classList.add('active');
      document.getElementById(target).classList.add('active');
    });
  });
</script>

<style scoped>
.login-container {
  width: 320px;
  margin: 100px auto;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  font-family: Arial, sans-serif;
}

/* 标签页样式 */
.tabs {
  display: flex;
  margin-bottom: 20px;
  border-bottom: 1px solid #eee;
}

.tab {
  padding: 10px 20px;
  cursor: pointer;
  font-size: 14px;
  color: #666;
  border-bottom: 2px solid transparent;
}

.tab.active {
  color: #007bff;
  border-bottom: 2px solid #007bff;
  font-weight: bold;
}

/* 内容区域 */
.tab-pane {
  display: none;
}

.tab-pane.active {
  display: block;
}
</style>

