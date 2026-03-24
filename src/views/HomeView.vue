<template>
  <div class="homeView">
    <!-- 侧边栏 (Sidebar) -->
    <aside class="sidebar glass-card">
      <div class="profile-section">
        <div class="avatar">
          <img
            src="../images/avatar.jpg"
            style="width: 100%; height: 100%; border-radius: 16px"
            alt=""
          />
        </div>
        <div class="user-info">
          <h2 class="username">baile</h2>
          <span class="status-badge">开发中</span>
        </div>
      </div>

      <nav class="nav-menu">
        <div class="nav-group">
          <h3 class="group-title">GENERAL</h3>
          <ul class="nav-list">
            <li
              v-for="item in navItems"
              :key="item.id"
              class="nav-item"
              :class="{ active: activeItem === item.id }"
              @click="setActive(item.id)"
            >
              <span class="icon">{{ item.icon }}</span>
              {{ item.label }}
            </li>
          </ul>
        </div>
      </nav>
    </aside>

    <!-- 主内容区 (Main Content) -->
    <main class="main-content">
      <div class="content-placeholder glass-card">
        <p>
          当前选中的是：<span style="color: #6366f1; font-weight: 600">{{ currentLabel }}</span>
        </p>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

// 定义导航项数据
const navItems = [
  { id: "recent", label: "近期文章", icon: "📄" },
  { id: "projects", label: "我的项目", icon: "🛠️" },
  { id: "about", label: "关于网站", icon: "👤" },
  { id: "recommend", label: "推荐分享", icon: "⭐" },
  { id: "blogs", label: "优秀博客", icon: "🎙️" },
];

// 当前选中的项 ID
const activeItem = ref("recent");

// 设置选中项的方法
const setActive = (id: string) => {
  activeItem.value = id;
};

// 计算当前选中的标签
const currentLabel = computed(() => {
  return navItems.find((item) => item.id === activeItem.value)?.label || "";
});
</script>

<style scoped>
.homeView {
  display: flex;
  gap: 24px;
  padding: 24px;
  min-height: 100vh;
  max-width: 1440px;
  margin: 0 auto;
}

/* 侧边栏样式 (Sidebar Styles) */
.sidebar {
  width: 220px;
  display: flex;
  flex-direction: column;
  padding: 32px 24px;
  flex-shrink: 0;
  height: calc(100vh - 48px);
  position: sticky;
  top: 24px;
}

.profile-section {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 48px;
}

.avatar {
  width: 56px;
  height: 56px;
  background: white;
  padding: 2px;
  border-radius: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.username {
  font-size: 1.25rem;
  font-weight: 700;
  color: #1e293b;
}

.status-badge {
  font-size: 0.75rem;
  padding: 2px 8px;
  background: rgba(45, 212, 191, 0.1);
  color: #0d9488;
  border-radius: 6px;
  font-weight: 600;
}

.nav-group {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.group-title {
  font-size: 0.75rem;
  color: #94a3b8;
  letter-spacing: 0.1em;
  font-weight: 700;
  margin-bottom: 8px;
}

.nav-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  border-radius: 16px;
  color: #64748b;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
}

.nav-item:hover {
  background: rgba(255, 255, 255, 0.4);
  color: #1e293b;
}

.nav-item.active {
  background: white;
  color: #1e293b;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.03);
}

.icon {
  font-size: 1.25rem;
}

/* 主内容区样式 (Main Content Styles) */
.main-content {
  flex-grow: 1;
}

.content-placeholder {
  height: 100%;
  padding: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #94a3b8;
  border-style: solid;
  border-color: rgba(0, 0, 0, 0.1);
}

/* 响应式适配 (Responsive) */
@media (max-width: 500px) {
  .homeView {
    flex-direction: column;
  }
  .sidebar {
    width: 100%;
    height: auto;
    position: static;
  }
}
</style>
