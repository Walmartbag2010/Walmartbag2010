<span style="color:#000caf;">**Hi!Here is my blog!👋**</span>
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=4877189&auto=1&height=66"></iframe>
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>地生中考倒计时（带进度条）</title>
  <script src="https://unpkg.com/@tailwindcss/browser@4"></script>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css" rel="stylesheet">
  <style type="text/tailwindcss">
    @theme {
      --color-primary: #3b82f6;
      --color-secondary: #1e40af;
      --color-accent: #93c5fd;
      --color-progress: #10b981;
      --color-progress-bg: #e5e7eb;
      --font-inter: 'Inter', sans-serif;
    }
    
    @utility smooth-transition {
      transition: all 0.3s ease-in-out;
    }
    
    @utility countdown-box {
      @apply bg-white rounded-lg shadow-md p-4 md:p-6 smooth-transition;
    }
    
    @utility time-unit {
      @apply flex flex-col items-center justify-center;
    }
    
    @utility time-value {
      @apply text-3xl md:text-4xl font-bold text-primary mb-2 smooth-transition;
    }
    
    @utility time-label {
      @apply text-sm md:text-base text-gray-600 smooth-transition;
    }
    
    @utility progress-container {
      @apply w-full bg-[var(--color-progress-bg)] rounded-full h-4 overflow-hidden mb-6 smooth-transition;
    }
    
    @utility progress-bar {
      @apply h-full bg-[var(--color-progress)] rounded-full smooth-transition;
    }
  </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-50 min-h-screen font-inter flex items-center justify-center p-4">
  <div class="max-w-md w-full bg-white rounded-xl shadow-lg p-6 md:p-8 smooth-transition">
    <div class="text-center mb-6">
      <h1 class="text-2xl md:text-3xl font-bold text-secondary mb-2">地生中考倒计时</h1>
      <p class="text-gray-600" id="exam-date">2025年6月30日 14:00</p>
    </div>
    
    <!-- 进度条组件 -->
    <div class="progress-container">
      <div class="progress-bar" id="progress-bar" style="width: 100%"></div>
    </div>
    <p class="text-sm text-gray-500 text-center mb-6" id="progress-text">100% 剩余</p>
    
    <div class="countdown-box mb-6">
      <div class="grid grid-cols-4 gap-4 md:gap-6">
        <div class="time-unit">
          <div class="time-value" id="days">00</div>
          <div class="time-label">天</div>
        </div>
        <div class="time-unit">
          <div class="time-value" id="hours">00</div>
          <div class="time-label">时</div>
        </div>
        <div class="time-unit">
          <div class="time-value" id="minutes">00</div>
          <div class="time-label">分</div>
        </div>
        <div class="time-unit">
          <div class="time-value" id="seconds">00</div>
          <div class="time-label">秒</div>
        </div>
      </div>
    </div>
    
    <div class="text-center">
      <p class="text-gray-600 mb-4">每一分努力，都在靠近成功！</p>
      <div class="flex justify-center space-x-4">
        <i class="fas fa-graduation-cap text-accent text-xl"></i>
        <i class="fas fa-clock text-accent text-xl"></i>
        <i class="fas fa-star text-accent text-xl"></i>
      </div>
    </div>
  </div>

  <script>
    // 设置考试时间（年-月-日 时:分:秒）
    const examTime = new Date('2025-06-30T14:00:00');
    const totalMs = examTime - new Date('2025-06-22T00:00:00'); // 总时间（从6月22日0点开始计算）
    
    function updateCountdown() {
      const now = new Date();
      const diff = examTime - now;
      
      // 检查是否已过考试时间
      if (diff <= 0) {
        updateUI(0, '考试已结束');
        return;
      }
      
      // 计算剩余时间
      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
      const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((diff % (1000 * 60)) / 1000);
      
      // 计算进度条百分比
      const progressPercent = (diff / totalMs) * 100;
      const progressText = `${Math.round(progressPercent)}% 剩余`;
      
      // 更新显示（补零处理）
      updateUI(progressPercent, progressText, days, hours, minutes, seconds);
    }
    
    function updateUI(progressPercent, progressText, days, hours, minutes, seconds) {
      document.getElementById('days').textContent = days.toString().padStart(2, '0');
      document.getElementById('hours').textContent = hours.toString().padStart(2, '0');
      document.getElementById('minutes').textContent = minutes.toString().padStart(2, '0');
      document.getElementById('seconds').textContent = seconds.toString().padStart(2, '0');
      document.getElementById('progress-bar').style.width = `${progressPercent}%`;
      document.getElementById('progress-text').textContent = progressText;
    }
    
    // 初始化倒计时
    updateCountdown();
    // 每秒更新一次
    setInterval(updateCountdown, 1000);
  </script>
</body>
</html>
