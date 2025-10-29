<template>
  <div class="taobao-login-page">
    <!-- 顶部 Logo -->
    <div class="header">
      <img src="https://via.placeholder.com/80x40/FF4D4F/FFFFFF?text=淘宝" alt="淘宝" class="logo" />
      <div class="top-right">
        <span>网站无障碍</span>
        <a href="#" class="feedback">"登录页面"改进建议</a>
      </div>
    </div>

    <!-- 登录卡片 -->
    <div class="login-card">
      <!-- 扫码登录区域 -->
      <div class="scan-section">
        <h3>手机扫码登录</h3>
        <div class="qr-code-container">
          <div class="qr-placeholder">
            <img src="https://via.placeholder.com/160x160/eeeeee/999999?text= 二维码" alt="二维码" class="qr-code" />
            <div class="expired-text">二维码已失效</div>
            <button class="refresh-btn">刷新</button>
          </div>
        </div>
        <p class="scan-tip">打开<span class="app-name">淘宝APP</span>—点击左上角扫一扫</p>
        <p class="help-link">怎么扫码登录？</p>
      </div>

      <!-- 登录区域（短信/密码切换） -->
      <div class="sms-section">
        <!-- 登录方式切换 -->
        <div class="tab-switch">
          <span class="tab" :class="{active: currentTab==='password'}" @click="switchTab('password')">密码登录</span>
          <span class="tab" :class="{active: currentTab==='sms'}" @click="switchTab('sms')">短信登录</span>
        </div>

        <!-- 手机号输入（两种方式都显示） -->
        <div class="input-group">
          <select class="country-code">
            <option value="+86">+86</option>
            <option value="+852">+852</option>
            <option value="+853">+853</option>
          </select>
          <input
            v-model="phone"
            type="tel"
            placeholder="请输入手机号"
            class="input-field"
          />
        </div>

        <!-- 动态切换表单内容 -->
        <div v-if="currentTab==='sms'">
          <div class="input-group">
            <input
              v-model="code"
              type="text"
              placeholder="请输入验证码"
              class="input-field"
            />
            <button class="get-code-btn" @click="getCode">获取验证码</button>
          </div>
        </div>
        <div v-else>
          <div class="input-group">
            <input
              v-model="password"
              type="password"
              placeholder="请输入密码"
              class="input-field"
            />
          </div>
        </div>

        <!-- 登录按钮 -->
        <button class="login-btn">登录</button>

        <!-- 额外选项 -->
        <div class="options">
          <a href="#" class="remember-me">忘记账号</a>
          <a href="#" class="register-link">免费注册</a>
        </div>

        <!-- 协议勾选 -->
        <div class="agreement">
          <input type="checkbox" id="agree" v-model="agreed" />
          <label for="agree" class="agree-text">
            已阅读并同意以下协议：<a href="#" class="link">淘宝平台服务协议</a>、<a href="#" class="link">隐私权政策</a>、<a href="#" class="link">法律声明</a>、<a href="#" class="link">支付宝及客户端服务协议</a>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 数据绑定
const phone = ref('')
const code = ref('')
const password = ref('') // 新增密码字段
const agreed = ref(false)

// 切换登录方式
const currentTab = ref('sms')

const switchTab = (type) => {
  currentTab.value = type
}

// 模拟获取验证码
const getCode = () => {
  if (!phone.value) {
    alert('请输入手机号')
    return
  }
  // 这里可以调用 API 发送验证码
  alert(`验证码已发送至 ${phone.value}`)
}
</script>

<style scoped>
.taobao-login-page {
  width: 100%;
  height: 100vh;
  background-color: #f5f5f5;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: 'Microsoft YaHei', sans-serif;
}

.header {
  width: 100%;
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
}

.logo {
  width: 80px;
  height: 40px;
}

.top-right {
  color: #666;
  font-size: 12px;
}

.feedback {
  color: #ff4d4f;
  text-decoration: none;
  margin-left: 10px;
}

.login-card {
  width: 700px;
  background-color: white;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  display: flex;
  box-sizing: border-box;
}

.scan-section {
  flex: 1;
  padding: 40px 30px;
  border-right: 1px solid #eaeaea;
  text-align: center;
}

.scan-section h3 {
  font-size: 18px;
  color: #333;
  margin-bottom: 20px;
}

.qr-code-container {
  width: 160px;
  height: 160px;
  margin: 0 auto;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  position: relative;
}

.qr-placeholder {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #999;
  font-size: 14px;
}

.qr-code {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.expired-text {
  margin-top: 10px;
  font-size: 14px;
  color: #666;
}

.refresh-btn {
  margin-top: 10px;
  padding: 8px 20px;
  background-color: #fff;
  color: #666;
  border: 1px solid #ddd;
  border-radius: 20px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.2s;
}

.refresh-btn:hover {
  background-color: #f5f5f5;
}

.scan-tip {
  font-size: 12px;
  color: #999;
  margin: 15px 0;
  text-align: center;
}

.app-name {
  color: #ff4d4f;
}

.help-link {
  font-size: 12px;
  color: #666;
  cursor: pointer;
  margin-top: 10px;
}

.sms-section {
  flex: 1;
  padding: 40px 30px;
  text-align: center;
}

.tab-switch {
  display: flex;
  justify-content: center;
  gap: 30px;
  margin-bottom: 20px;
}

.tab {
  font-size: 16px;
  cursor: pointer;
  transition: color 0.2s;
}

.tab.active {
  color: #ff4d4f;
  font-weight: bold;
}

.input-group {
  margin-bottom: 20px;
  position: relative;
  display: flex;
  align-items: center;
}

.input-group .input-field {
  flex: 1;
  min-width: 0;
}

.input-group .get-code-btn {
  position: static;
  margin-left: 16px;
  padding: 10px 15px;
  background-color: transparent;
  color: #ff4d4f;
  border: 1px solid #ff4d4f;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.country-code {
  width: 60px;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 6px 0 0 6px;
  background-color: #f5f5f5;
  outline: none;
  font-size: 14px;
}

.input-field {
  flex: 1;
  min-width: 0;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 0 6px 6px 0;
  font-size: 14px;
  outline: none;
  box-sizing: border-box;
}

.get-code-btn {
  position: static;
  margin-left: 16px;
  padding: 10px 15px;
  background-color: transparent;
  color: #ff4d4f;
  border: 1px solid #ff4d4f;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
  transition: background-color 0.2s;
  margin-left: 12px; /* 新增左侧间距 */
}

.login-btn {
  width: 100%;
  padding: 12px;
  background-color: #ff4d4f;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.login-btn:hover {
  background-color: #e53a3a;
}

.options {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin: 20px 0;
  font-size: 12px;
  color: #666;
}

.remember-me,
.register-link {
  text-decoration: none;
  cursor: pointer;
}

.agreement {
  margin-top: 10px;
  text-align: left;
  font-size: 12px;
  color: #666;
}

.agree-text {
  display: inline-block;
  margin-left: 5px;
}

.agree-text a {
  color: #ff4d4f;
  text-decoration: none;
}
</style>