<template>
  <div class="taobao-header">
    <!-- 顶部横幅 -->
    <div class="top-banner">
      <div class="banner-content">
        <a href="/promotion/double11" class="banner-link">
          <img src="#" alt="优惠券" class="banner-img" />
        </a>
        <span class="banner-text">天猫双11 大放价 爆款秒杀低至5折</span>
        <button class="btn-buy-now" @click="goToPromotion">立即抢购</button>
      </div>
    </div>

    <!-- 主体内容区 -->
    <div class="main-content">
      <!-- 淘宝 Logo -->
      <div class="logo">
        <a href="/" class="logo-link">
          <img src="#" alt="淘宝" class="logo-img" />
        </a>
      </div>

      <!-- 搜索区域 -->
      <div class="search-area">
        <div class="search-container">
          <!-- 分类选择 -->
          <select class="category-select">
            <option value="item">宝贝</option>
            <option value="shop">店铺</option>
            <option value="brand">品牌</option>
          </select>

          <!-- 输入框 -->
          <input
            v-model="searchQuery"
            type="text"
            placeholder="请输入关键词..."
            class="search-input"
          />

          <!-- 搜索按钮 -->
          <button class="search-btn">搜索</button>
        </div>

        <!-- 搜同款按钮 -->
        <button class="same-item-btn">
          <span>📷</span> 搜同款
        </button>
      </div>

      <!-- 右侧推广 -->
      <div class="right-promo">
        <div class="promo-text">
          <p>天天领元宝换红包</p>
          <p>开启淘江湖 > </p>
        </div>
        <img src="https://via.placeholder.com/80x80/FFD700/000000?text=小人" alt="小人" />
      </div>
    
      <!-- 帮助链接（位于最右） -->
      <div class="help-link">
        <a href="/help">寻求帮助</a>
      </div>
    </div>
  </div>
  <!-- 滚动图片 -->
  <div></div>
</template>

<script setup>
</script>

<style scoped>
.taobao-header {
  width: 100%;
  background: linear-gradient(to bottom, #ff4d4f, #fff);
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

/* 顶部横幅 */
.top-banner {
  background-color: #ff4d4f;
  color: white;
  text-align: center;
  padding: 10px 0;
  font-size: 18px;
  font-weight: bold;
  position: relative;
}

.banner-content {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

.banner-text {
  font-size: 22px;
  font-weight: 700;
}

.btn-buy-now {
  background-color: white;
  color: #ff4d4f;
  border: none;
  padding: 8px 20px;
  border-radius: 20px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-buy-now:hover {
  background-color: #f0f0f0;
}

/* 主体内容 */
.main-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 50px;
  max-width: 1400px;
  margin: 0 auto;
  background-color: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.logo {
  width: 120px;
  height: 60px;
}

.logo-link, .banner-link {
  display: block;
  text-decoration: none;
  cursor: pointer;
  transition: opacity 0.2s;
}

.logo-link:hover, .banner-link:hover {
  opacity: 0.8;
}

.logo-img, .banner-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

/* 搜索容器 */
.search-area {
  display: flex;
  align-items: center;
  gap: 15px;
  width: 100%;
  max-width: 800px;
}

.search-container {
  display: flex;
  align-items: center;
  flex: 1;
  border: 2px solid #ff4d4f;
  border-radius: 8px;
  overflow: hidden;
  background-color: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 0;
}

.category-select {
  background-color: transparent;
  border: none;
  padding: 12px 15px;
  font-size: 14px;
  cursor: pointer;
  outline: none;
  color: #333;
}

.search-input {
  flex: 1;
  padding: 12px 15px;
  border: none;
  font-size: 16px;
  outline: none;
  background-color: transparent;
  margin-right: 8px; /* 添加右侧间距 */
}

.search-btn {
  background-color: #ff4d4f;
  color: white;
  border: none;
  padding: 12px 35px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 20px; /* 增加圆角度数 */
  transition: background-color 0.2s;
  position: relative;
  margin: 6px; /* 添加按钮四周间距 */
}

.search-btn::after {
  content: '';
  position: absolute;
  right: -20px;
  top: 50%;
  transform: translateY(-50%);
  height: 70%;
  width: 1px;
  background-color: #ddd;
}

.search-btn:hover {
  background-color: #e53a3a;
}

.same-item-btn {
  background-color: white;
  color: #ff4d4f;
  border: 1px solid #ff4d4f;
  padding: 12px 20px;
  font-size: 14px;
  cursor: pointer;
  border-radius: 8px;
  margin-left: 30px;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: background-color 0.2s;
}

.same-item-btn:hover {
  background-color: #f9f9f9;
}

/* 右侧推广 */
.right-promo {
  display: flex;
  align-items: center;
  gap: 15px;
  font-size: 14px;
  color: #333;
}

.promo-text p {
  margin: 0;
}

.promo-text p:first-child {
  font-weight: bold;
  color: #ff4d4f;
}

/* 帮助链接样式，位于头部最右侧 */
.help-link {
  display: flex;
  align-items: center;
  margin-left: 20px;
}

.help-link a {
  color: #ff4d4f;
  text-decoration: none;
  font-weight: 600;
  padding: 6px 10px;
  border-radius: 6px;
}

.help-link a:hover {
  background-color: #fff5f5;
}
</style>