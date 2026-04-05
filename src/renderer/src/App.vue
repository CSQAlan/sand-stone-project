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
  background: rgba(0, 145, 255, 0.15) !important;
  border: 2px solid rgba(0, 168, 255, 0.5) !important;
  color: #00d2ff !important; /* 恢复为亮蓝色 */
  text-shadow: none !important;
  box-shadow: inset 0 0 10px rgba(0, 168, 255, 0.2) !important;
  transition: all 0.2s ease !important;
  position: relative;
  overflow: hidden;
  font-weight: bold !important;
  font-size: 16px !important; /* 保留加大字号 */
  letter-spacing: 1.2px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 10px 24px !important;
  text-transform: uppercase;
}

.tech-button:hover:not(.is-disabled) {
  background: rgba(0, 145, 255, 0.3) !important;
  border-color: #00ffff !important;
  box-shadow: 
    0 0 15px rgba(0, 210, 255, 0.4), 
    inset 0 0 10px rgba(0, 210, 255, 0.2) !important;
  transform: translateY(-2px);
  color: #ffffff !important; /* 悬停时依然变为纯白以增强交互感 */
}

/* Specific types */
.tech-button-success {
  background: rgba(103, 194, 58, 0.15) !important;
  border-color: rgba(103, 194, 58, 0.5) !important;
  color: #67c23a !important; /* 恢复为绿色 */
}

.tech-button-danger {
  background: rgba(245, 108, 108, 0.15) !important;
  border-color: rgba(245, 108, 108, 0.5) !important;
  color: #f56c6c !important; /* 恢复为红色 */
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

/* Global Element Plus Select Dropdown Styles */
.el-select__popper.el-popper {
  background: #001529 !important;
  border: 1px solid rgba(0, 145, 255, 0.4) !important;
  box-shadow: 0 0 15px rgba(0, 145, 255, 0.2) !important;
}

.el-select__popper.el-popper .el-popper__arrow::before {
  background: #001529 !important;
  border: 1px solid rgba(0, 145, 255, 0.4) !important;
}

.el-select-dropdown__item {
  color: #a5d8ff !important;
  font-weight: 500 !important;
}

.el-select-dropdown__item.hover,
.el-select-dropdown__item:hover {
  background: rgba(0, 145, 255, 0.2) !important;
  color: #ffffff !important;
}

.el-select-dropdown__item.selected {
  background: rgba(0, 145, 255, 0.3) !important;
  color: #00a8ff !important;
  font-weight: bold !important;
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
