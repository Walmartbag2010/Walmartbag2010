<span style="color:#000caf;">**Hi!Here is my blog!👋**</span>
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=4877189&auto=1&height=66"></iframe>

<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>地生中考倒计时（小时）</title>
  <script src="https://unpkg.com/@tailwindcss/browser@4"></script>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css" rel="stylesheet">
  <style type="text/tailwindcss">
    @theme {
      --color-primary: #4f46e5;
      --color-secondary: #7c3aed;
      --color-accent: #d8b4fe;
      --font-inter: 'Inter', system-ui, sans-serif;
    }
    
    @utility countdown-container {
      @apply relative w-full max-w-md mx-auto p-6 rounded-2xl overflow-hidden smooth-transition;
    }
    
    @utility bg-gradient {
      @apply bg-gradient-to-br from-[var(--color-primary)] to-[var(--color-secondary)];
    }
    
    @utility hour-display {
      @apply absolute inset-0 flex flex-col items-center justify-center;
    }
    
    @utility hour-number {
      @apply text-[clamp(5rem,12vw,8rem)] font-black text-white leading-tight smooth-transition;
    }
    
    @utility hour-label {
      @apply text-[clamp(1rem,3vw,1.5rem)] text-[var(--color-accent)] mt-4 smooth-transition;
    }
    
    @utility shadow-effect {
      @apply shadow-2xl shadow-[var(--color-primary)/20] backdrop-blur-md;
    }
  </style>
</head>
<body class="bg-gray-50 min-h-screen flex items-center justify-center p-4 font-inter">
  <div class="countdown-container shadow-effect bg-gradient">
    <div class="hour-display" id="countdown">
      <div class="hour-number" id="hours">000</div>
      <div class="hour-label">小时后考试</div>
    </div>
    <div class="absolute bottom-4 left-0 right-0 text-center">
      <p class="text-white/80 text-sm md:text-base" id="exam-date">2025年6月30日 14:00</p>
    </div>
  </div>

  <script>
    // 设置考试时间（年-月-日 时:分:秒）
    const examTime = new Date('2025-06-30T14:00:00');
    
    function updateCountdown() {
      const now = new Date();
      const diff = examTime - now;
      
      // 检查是否已过考试时间
      if (diff <= 0) {
        document.getElementById('hours').textContent = '0';
        document.getElementById('hour-label').textContent = '考试进行中';
        document.getElementById('exam-date').textContent = '2025年6月30日 已开始';
        return;
      }
      
      // 计算剩余小时数（四舍五入）
      const hours = Math.round(diff / (1000 * 60 * 60));
      
      // 更新显示
      const hoursElement = document.getElementById('hours');
      hoursElement.textContent = hours;
      
      // 添加数字变化动画
      hoursElement.classList.add('scale-110');
      setTimeout(() => {
        hoursElement.classList.remove('scale-110');
      }, 300);
    }
    
    // 初始化倒计时
    updateCountdown();
    // 每10分钟更新一次（减少性能消耗）
    setInterval(updateCountdown, 1000 * 60 * 10);
    // 额外每秒检查一次，确保准点更新
    setInterval(() => {
      const now = new Date();
      if (now.getMinutes() === 0 && now.getSeconds() === 0) {
        updateCountdown();
      }
    }, 1000);
  </script>
</body>
</html>
    }
    
    // 初始化倒计时
    updateCountdown();
    // 每秒更新一次
    setInterval(updateCountdown, 1000);
  </script>
</body>
</html>
