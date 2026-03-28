<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>中考倒计时</title>
    <style>
        body {
            margin: 0;
            padding: 20px;
            background-color: #f0f0f0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            font-family: 'Arial', sans-serif;
        }
        .title {
            font-size: 24px;
            color: #333;
            margin-bottom: 30px;
            text-align: center;
        }
        .countdown {
            display: flex;
            gap: 15px;
            align-items: baseline;
        }
        .time-box {
            text-align: center;
        }
        .time-number {
            font-size: clamp(3rem, 15vw, 8rem);
            font-weight: bold;
            color: #222;
            line-height: 1;
        }
        .time-label {
            font-size: clamp(1rem, 3vw, 1.5rem);
            color: #666;
            text-transform: uppercase;
        }
        .separator {
            font-size: clamp(2rem, 8vw, 5rem);
            color: #999;
            line-height: 1;
        }
        .target-date {
            margin-top: 30px;
            font-size: 16px;
            color: #777;
        }
        .extra-hours {
            margin-top: 12px;
            font-size: 14px;
            color: #888;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="title">距离中考还有</div>
    <div class="countdown">
        <div class="time-box">
            <div class="time-number" id="days">00</div>
            <div class="time-label">天</div>
        </div>
        <div class="separator">:</div>
        <div class="time-box">
            <div class="time-number" id="hours">00</div>
            <div class="time-label">时</div>
        </div>
        <div class="separator">:</div>
        <div class="time-box">
            <div class="time-number" id="minutes">00</div>
            <div class="time-label">分</div>
        </div>
        <div class="separator">:</div>
        <div class="time-box">
            <div class="time-number" id="seconds">00</div>
            <div class="time-label">秒</div>
        </div>
    </div>
    <div class="target-date">考试时间：2026年6月26日 09:30</div>
    <div class="extra-hours" id="extraHours"></div>
    <script>
        // 目标时间：2026年6月26日 09:30:00（注意月份从0开始，5代表6月）
        const targetTime = new Date(2026, 5, 26, 9, 30, 0);
        const daysElement = document.getElementById('days');
        const hoursElement = document.getElementById('hours');
        const minutesElement = document.getElementById('minutes');
        const secondsElement = document.getElementById('seconds');
        const extraHoursElement = document.getElementById('extraHours');
        function updateCountdown() {
            const now = new Date();
            const diffMs = targetTime - now;
            if (diffMs <= 0) {
                daysElement.textContent = '00';
                hoursElement.textContent = '00';
                minutesElement.textContent = '00';
                secondsElement.textContent = '00';
                extraHoursElement.textContent = '';
                document.querySelector('.title').textContent = '中学时代已结束';
                return;
            }
            const totalSeconds = Math.floor(diffMs / 1000);
            const days = Math.floor(totalSeconds / (3600 * 24));
            const hours = Math.floor((totalSeconds % (3600 * 24)) / 3600);
            const minutes = Math.floor((totalSeconds % 3600) / 60);
            const seconds = totalSeconds % 60;           
            // 计算剩余总小时数（向下取整）
            const totalHours = Math.floor(totalSeconds / 3600);  
            daysElement.textContent = days.toString().padStart(2, '0');
            hoursElement.textContent = hours.toString().padStart(2, '0');
            minutesElement.textContent = minutes.toString().padStart(2, '0');
            secondsElement.textContent = seconds.toString().padStart(2, '0');
            // 更新下方小字
            extraHoursElement.textContent = `剩余总小时数：${totalHours} 小时`;
        }
        updateCountdown();
        setInterval(updateCountdown, 1000);
    </script>
</body>
</html>
