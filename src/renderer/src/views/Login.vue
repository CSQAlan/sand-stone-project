<template>
  <div class="login-page" @mousemove="handleMouseMove">
    <!-- 电子扫描线滤镜 -->
    <div class="scanlines"></div>
    
    <!-- 背景光晕 -->
    <div class="bg-glow"></div>

    <!-- 粒子背景 -->
    <div id="particles-js" class="particles-container"></div>

    <!-- 登录区域容器 -->
    <div 
      class="login-container" 
      :style="parallaxStyle"
    >
      <!-- 流光边框装饰 -->
      <div class="border-flow"></div>

      <!-- 左侧信息区 -->
      <div class="login-info">
        <div class="logo-area animate-in" style="--delay: 0.1s">
          <div class="logo-icon">
            <el-icon><Monitor /></el-icon>
            <div class="icon-glow"></div>
          </div>
        </div>
        
        <div class="title-group animate-in" style="--delay: 0.2s">
          <h1 class="system-title">砂石级配实验监控平台</h1>
          <p class="system-subtitle">Sand Gradation Digital Lab System</p>
        </div>

        <div class="info-features animate-in" style="--delay: 0.3s">
          <div class="feature-item">
            <el-icon><DataAnalysis /></el-icon>
            <div class="feature-text">
              <span class="label">实时监控</span>
              <span class="desc">Real-time Data Flow</span>
            </div>
          </div>
          <div class="feature-item">
            <el-icon><PictureFilled /></el-icon>
            <div class="feature-text">
              <span class="label">图像识别</span>
              <span class="desc">AI Vision Analysis</span>
            </div>
          </div>
          <div class="feature-item">
            <el-icon><Histogram /></el-icon>
            <div class="feature-text">
              <span class="label">智能报表</span>
              <span class="desc">Automated Reports</span>
            </div>
          </div>
        </div>
        
        <!-- 底部装饰线 -->
        <div class="info-decoration animate-in" style="--delay: 0.4s">
          <div class="line"></div>
          <div class="dots"><span></span><span></span><span></span></div>
        </div>
      </div>

      <!-- 右侧登录表单 -->
      <div class="login-form-area animate-in" style="--delay: 0.2s">
        <div class="login-form-container">
          <div class="form-header">
            <h2 class="welcome-text">用户认证</h2>
            <div class="auth-tag">AUTH REQUIRED</div>
          </div>
          <p class="login-desc">请扫描权限凭证或输入访问代码</p>

          <el-form
            ref="loginFormRef"
            :model="loginForm"
            :rules="loginRules"
            class="login-form"
            size="large"
          >
            <el-form-item prop="username" class="animate-in" style="--delay: 0.4s">
              <el-input
                v-model="loginForm.username"
                placeholder="USERNAME"
                :prefix-icon="User"
                clearable
                @keyup.enter="handleLogin"
              />
            </el-form-item>

            <el-form-item prop="password" class="animate-in" style="--delay: 0.5s">
              <el-input
                v-model="loginForm.password"
                type="password"
                placeholder="PASSWORD"
                :prefix-icon="Lock"
                show-password
                clearable
                @keyup.enter="handleLogin"
              />
            </el-form-item>

            <div class="login-options animate-in" style="--delay: 0.6s">
              <el-checkbox v-model="rememberMe" class="tech-checkbox">记住授权</el-checkbox>
              <el-button type="text" class="forgot-password">找回密钥</el-button>
            </div>

            <el-form-item class="animate-in" style="--delay: 0.7s">
              <el-button
                type="primary"
                class="login-button"
                :loading="loading"
                @click="handleLogin"
              >
                <span class="btn-text">确认进入系统</span>
                <div class="btn-glow"></div>
              </el-button>
            </el-form-item>
          </el-form>

          <div class="login-footer animate-in" style="--delay: 0.8s">
            <div class="terminal-info">
              <span>NODE: 127.0.0.1</span>
              <span>STATUS: READY</span>
            </div>
            <p class="copyright">© 2026 DIGITAL SAND LAB - VERSION 1.0.0</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, computed } from 'vue'
import { useRouter } from 'vue-router'
import { ElMessage } from 'element-plus'
import {
  User,
  Lock,
  Monitor,
  DataAnalysis,
  PictureFilled,
  Histogram
} from '@element-plus/icons-vue'

const router = useRouter()
const loginFormRef = ref(null)
const loading = ref(false)
const rememberMe = ref(false)

// 鼠标悬浮视差
const mousePos = reactive({ x: 0, y: 0 })
const handleMouseMove = (e) => {
  const { clientX, clientY } = e
  const { innerWidth, innerHeight } = window
  mousePos.x = (clientX - innerWidth / 2) / (innerWidth / 2)
  mousePos.y = (clientY - innerHeight / 2) / (innerHeight / 2)
}

const parallaxStyle = computed(() => {
  const rotateY = mousePos.x * 5 // 最大旋转5度
  const rotateX = -mousePos.y * 5
  return {
    transform: `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`
  }
})

// 登录表单数据
const loginForm = reactive({
  username: '',
  password: ''
})

// 表单验证规则
const loginRules = {
  username: [
    { required: true, message: '请输入用户名', trigger: 'blur' }
  ],
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' }
  ]
}

// 处理登录
const handleLogin = () => {
  loginFormRef.value.validate((valid) => {
    if (!valid) return

    loading.value = true

    // 模拟登录请求
    setTimeout(() => {
      if (loginForm.username === 'admin' && loginForm.password === '123456') {
        ElMessage({
          message: '身份验证成功，正在同步实验室数据...',
          type: 'success',
          customClass: 'tech-message'
        })

        localStorage.setItem('isLoggedIn', 'true')
        if (rememberMe.value) {
          localStorage.setItem('username', loginForm.username)
        } else {
          localStorage.removeItem('username')
        }

        setTimeout(() => {
          router.push('/dashboard')
        }, 1000)
      } else {
        ElMessage({
          message: '权限验证失败：无效的凭证',
          type: 'error',
          customClass: 'tech-message'
        })
      }
      loading.value = false
    }, 1500)
  })
}

const checkRememberedUser = () => {
  const rememberedUsername = localStorage.getItem('username')
  if (rememberedUsername) {
    loginForm.username = rememberedUsername
    rememberMe.value = true
  }
}

const initParticles = () => {
  const script = document.createElement('script')
  script.src = 'https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js'
  script.onload = () => {
    window.particlesJS('particles-js', {
      particles: {
        number: { value: 60, density: { enable: true, value_area: 800 } },
        color: { value: '#00a8ff' },
        shape: { type: 'circle' },
        opacity: {
          value: 0.2,
          random: true,
          anim: { enable: true, speed: 1, opacity_min: 0.1 }
        },
        size: {
          value: 2,
          random: true,
          anim: { enable: true, speed: 2, size_min: 0.1 }
        },
        line_linked: {
          enable: true,
          distance: 150,
          color: '#00a8ff',
          opacity: 0.1,
          width: 1
        },
        move: {
          enable: true,
          speed: 0.6,
          direction: 'none',
          random: true,
          out_mode: 'out'
        }
      },
      interactivity: {
        detect_on: 'canvas',
        events: {
          onhover: { enable: true, mode: 'grab' },
          resize: true
        },
        modes: {
          grab: { distance: 140, line_linked: { opacity: 0.4 } }
        }
      },
      retina_detect: true
    })
  }
  document.body.appendChild(script)
}

onMounted(() => {
  checkRememberedUser()
  initParticles()
})
</script>

<style scoped>
.login-page {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #000814;
  position: relative;
  overflow: hidden;
  font-family: 'Inter', 'Segoe UI', sans-serif;
}

/* 扫描线效果 */
.scanlines {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    rgba(18, 16, 16, 0) 50%,
    rgba(0, 0, 0, 0.1) 50%
  ), linear-gradient(
    90deg,
    rgba(255, 0, 0, 0.02),
    rgba(0, 255, 0, 0.01),
    rgba(0, 0, 255, 0.02)
  );
  background-size: 100% 3px, 3px 100%;
  z-index: 10;
  pointer-events: none;
}

/* 背景光晕 */
.bg-glow {
  position: absolute;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at 50% 50%, #001f3f 0%, transparent 70%);
  opacity: 0.5;
  z-index: 2;
}

.particles-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 3;
}

/* 登录容器 */
.login-container {
  display: flex;
  width: 1000px;
  height: 600px;
  background: rgba(0, 18, 36, 0.6);
  backdrop-filter: blur(20px);
  border-radius: 4px; /* 工业风更偏向直角或微圆角 */
  border: 1px solid rgba(0, 168, 255, 0.1);
  box-shadow: 0 0 50px rgba(0, 0, 0, 0.8);
  overflow: hidden;
  z-index: 20;
  position: relative;
  transition: transform 0.1s ease-out;
}

/* 流光边框 */
.border-flow {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  border: 1px solid transparent;
  mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  mask-composite: exclude;
  z-index: 21;
}

.border-flow::before {
  content: '';
  position: absolute;
  width: 200%;
  height: 200%;
  top: -50%;
  left: -50%;
  background: conic-gradient(
    transparent, 
    transparent, 
    transparent, 
    #00a8ff
  );
  animation: rotate 4s linear infinite;
}

@keyframes rotate {
  100% { transform: rotate(360deg); }
}

/* 左侧信息区域 */
.login-info {
  flex: 1;
  padding: 60px 50px;
  display: flex;
  flex-direction: column;
  background: rgba(0, 40, 80, 0.1);
  border-right: 1px solid rgba(0, 168, 255, 0.1);
}

.logo-icon {
  width: 70px;
  height: 70px;
  background: rgba(0, 168, 255, 0.05);
  border: 1px solid rgba(0, 168, 255, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.logo-icon :deep(svg) {
  font-size: 36px;
  color: #00a8ff;
  z-index: 2;
}

.icon-glow {
  position: absolute;
  width: 100%;
  height: 100%;
  background: #00a8ff;
  filter: blur(15px);
  opacity: 0.2;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 0.1; }
  50% { opacity: 0.3; }
}

.system-title {
  font-size: 26px;
  font-weight: 700;
  color: #fff;
  margin: 30px 0 5px 0;
  letter-spacing: 3px;
  background: linear-gradient(to right, #fff, #00a8ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.system-subtitle {
  font-size: 12px;
  color: rgba(0, 168, 255, 0.6);
  letter-spacing: 1px;
  text-transform: uppercase;
}

.info-features {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 20px;
}

.feature-item :deep(svg) {
  font-size: 20px;
  color: #00a8ff;
  opacity: 0.8;
}

.feature-text {
  display: flex;
  flex-direction: column;
}

.feature-text .label {
  color: #fff;
  font-size: 15px;
  font-weight: 500;
}

.feature-text .desc {
  color: rgba(255, 255, 255, 0.3);
  font-size: 11px;
}

.info-decoration {
  margin-top: auto;
  display: flex;
  align-items: center;
  gap: 15px;
}

.info-decoration .line {
  height: 1px;
  flex: 1;
  background: linear-gradient(to right, #00a8ff, transparent);
}

.info-decoration .dots span {
  display: inline-block;
  width: 4px;
  height: 4px;
  background: #00a8ff;
  margin-right: 5px;
  border-radius: 50%;
}

/* 右侧表单区域 */
.login-form-area {
  width: 420px;
  padding: 60px 45px;
  background: rgba(0, 10, 20, 0.4);
}

.form-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 10px;
}

.welcome-text {
  font-size: 24px;
  color: #fff;
  margin: 0;
}

.auth-tag {
  font-size: 10px;
  color: #00a8ff;
  padding: 2px 6px;
  border: 1px solid #00a8ff;
  border-radius: 2px;
}

.login-desc {
  font-size: 13px;
  color: rgba(255, 255, 255, 0.4);
  margin-bottom: 40px;
}

.login-form :deep(.el-input__wrapper) {
  background: rgba(0, 168, 255, 0.05) !important;
  border: 1px solid rgba(0, 168, 255, 0.2) !important;
  box-shadow: none !important;
  border-radius: 2px;
}

.login-form :deep(.el-input__wrapper.is-focus) {
  border-color: #00a8ff !important;
  background: rgba(0, 168, 255, 0.1) !important;
}

.login-form :deep(.el-input__inner) {
  color: #fff;
  letter-spacing: 1px;
}

.login-options {
  display: flex;
  justify-content: space-between;
  margin-bottom: 30px;
}

.tech-checkbox {
  --el-checkbox-text-color: rgba(255, 255, 255, 0.5);
  --el-checkbox-checked-text-color: #00a8ff;
}

.forgot-password {
  color: rgba(0, 168, 255, 0.6);
  font-size: 12px;
}

.login-button {
  width: 100%;
  height: 48px;
  background: transparent !important;
  border: 1px solid #00a8ff !important;
  color: #00a8ff !important;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 2px;
  position: relative;
  overflow: hidden;
  border-radius: 2px;
}

.login-button:hover {
  background: #00a8ff !important;
  color: #000 !important;
  box-shadow: 0 0 20px rgba(0, 168, 255, 0.4);
}

.login-footer {
  margin-top: 50px;
}

.terminal-info {
  display: flex;
  justify-content: space-between;
  font-size: 10px;
  color: rgba(0, 168, 255, 0.3);
  font-family: monospace;
  margin-bottom: 5px;
}

.copyright {
  font-size: 10px;
  color: rgba(255, 255, 255, 0.2);
  text-align: center;
}

/* 入场动画 */
.animate-in {
  opacity: 0;
  transform: translateY(20px);
  animation: slideUp 0.8s forwards;
  animation-delay: var(--delay);
}

@keyframes slideUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 响应式调整 */
@media (max-width: 1024px) {
  .login-container { width: 95%; height: auto; flex-direction: column; }
  .login-info { padding: 40px; }
  .login-form-area { width: 100%; padding: 40px; }
}
</style>
