<template>
  <div class="app-container">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: #001529;
  overflow: hidden;
}

/* 全局隐藏所有滚动条 - Webkit浏览器 (Chrome, Safari, Edge, Electron) */
::-webkit-scrollbar {
  width: 0 !important;
  height: 0 !important;
  display: none !important;
}

::-webkit-scrollbar-track {
  display: none !important;
}

::-webkit-scrollbar-thumb {
  display: none !important;
}

/* 隐藏滚动条 - Firefox */
* {
  scrollbar-width: none !important;
}

/* 隐藏滚动条 - IE/Edge */
* {
  -ms-overflow-style: none !important;
}

#app {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

/* Unified Tech Button Style */
.tech-button {
  background: rgba(0, 145, 255, 0.1) !important;
  border: 1px solid rgba(0, 145, 255, 0.4) !important;
  color: #00a8ff !important;
  text-shadow: 0 0 8px rgba(0, 168, 255, 0.5);
  box-shadow: inset 0 0 15px rgba(0, 145, 255, 0.1);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1) !important;
  position: relative;
  overflow: hidden;
  font-weight: 500;
  letter-spacing: 1px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.tech-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(0, 168, 255, 0.2),
    transparent
  );
  transition: 0.5s;
}

.tech-button:hover::before {
  left: 100%;
}

.tech-button:hover:not(.is-disabled) {
  background: rgba(0, 145, 255, 0.2) !important;
  border-color: #00a8ff !important;
  box-shadow: 0 0 15px rgba(0, 168, 255, 0.4), inset 0 0 10px rgba(0, 168, 255, 0.2) !important;
  transform: translateY(-1px);
}

.tech-button:active:not(.is-disabled) {
  transform: translateY(1px);
  box-shadow: 0 0 5px rgba(0, 168, 255, 0.4) !important;
}

/* Specific types */
.tech-button-success {
  background: rgba(103, 194, 58, 0.1) !important;
  border-color: rgba(103, 194, 58, 0.4) !important;
  color: #67c23a !important;
}
.tech-button-success:hover:not(.is-disabled) {
  background: rgba(103, 194, 58, 0.2) !important;
  border-color: #67c23a !important;
  box-shadow: 0 0 15px rgba(103, 194, 58, 0.4) !important;
}

.tech-button-danger {
  background: rgba(245, 108, 108, 0.1) !important;
  border-color: rgba(245, 108, 108, 0.4) !important;
  color: #f56c6c !important;
}
.tech-button-danger:hover:not(.is-disabled) {
  background: rgba(245, 108, 108, 0.2) !important;
  border-color: #f56c6c !important;
  box-shadow: 0 0 15px rgba(245, 108, 108, 0.4) !important;
}

.tech-button-info {
  background: rgba(144, 147, 153, 0.1) !important;
  border-color: rgba(144, 147, 153, 0.4) !important;
  color: #909399 !important;
}
.tech-button-info:hover:not(.is-disabled) {
  background: rgba(144, 147, 153, 0.2) !important;
  border-color: #909399 !important;
  box-shadow: 0 0 15px rgba(144, 147, 153, 0.4) !important;
}

/* Disabled state */
.tech-button.is-disabled {
  opacity: 0.5;
  cursor: not-allowed;
  background: rgba(255, 255, 255, 0.05) !important;
  border-color: rgba(255, 255, 255, 0.1) !important;
  color: rgba(255, 255, 255, 0.3) !important;
  box-shadow: none !important;
}

.app-container {
  height: 100%;
  padding: 10px;
  overflow: hidden;
}

/* Element Plus 组件滚动条隐藏 */
.el-scrollbar__wrap {
  overflow-x: hidden !important;
}

.el-scrollbar__wrap::-webkit-scrollbar {
  display: none !important;
}

/* 表格滚动条隐藏 */
.el-table__body-wrapper::-webkit-scrollbar {
  display: none !important;
}

/* 下拉框滚动条隐藏 */
.el-select-dropdown__wrap::-webkit-scrollbar {
  display: none !important;
}
</style>
