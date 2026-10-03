<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>中華職棒賽程看板</title>
  <!-- 引入 FontAwesome 圖標 -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    }

    body {
      background-color: #f0f2f5;
      color: #333;
    }

    /* 頂部導覽列 */
    header {
      background-color: #ffffff;
      border-bottom: 1px solid #e5e7eb;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
    }

    .nav-container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 16px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 64px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      font-size: 24px;
      font-weight: 900;
      color: #0b4f8c;
      letter-spacing: 1px;
    }

    .nav-menu {
      display: flex;
      gap: 20px;
      list-style: none;
      font-weight: 600;
      font-size: 15px;
    }

    .nav-menu li a {
      text-decoration: none;
      color: #4b5563;
      transition: color 0.2s;
    }

    .nav-menu li a:hover, .nav-menu li a.active {
      color: #0b4f8c;
    }

    /* 主要內容容器 */
    .container {
      max-width: 1000px;
      margin: 24px auto;
      padding: 0 16px;
    }

    /* 日期控制列與軍別切換 */
    .controls-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 24px;
      flex-wrap: wrap;
      gap: 16px;
    }

    /* 日期文字顏色改為深藍色 */
    .date-selector {
      display: flex;
      align-items: center;
      gap: 16px;
      font-size: 22px;
      font-weight: 800;
      color: #0b4f8c; /* 已修改為深藍色 */
    }

    .date-btn {
      background: none;
      border: none;
      font-size: 20px;
      cursor: pointer;
      color: #0b4f8c; /* 箭頭同步深藍色 */
      padding: 4px 8px;
    }

    .date-btn:hover {
      color: #052648; /* 滑鼠懸停時稍微加深 */
    }

    .toggle-group {
      display: flex;
      background: #e5e7eb;
      border-radius: 4px;
      overflow: hidden;
    }

    .toggle-btn {
      padding: 8px 24px;
      border: none;
      background: transparent;
      font-weight: 700;
      cursor: pointer;
      color: #4b5563;
      transition: 0.2s;
    }

    .toggle-btn.active {
      background-color: #374151;
      color: #ffffff;
    }

    /* 比賽卡片列表 */
    .games-list {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .game-card {
      background-color: #ffffff;
      border-radius: 6px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
      display: grid;
      grid-template-columns: 70px 1fr 120px 140px 180px 110px;
      align-items: center;
      padding: 16px 20px;
      border-left: 4px solid #0b4f8c;
    }

    /* 場次編號 */
    .game-id {
      background: #f3f4f6;
      border: 1px solid #d1d5db;
      border-radius: 20px;
      padding: 4px 8px;
      font-size: 13px;
      font-weight: 700;
      color: #6b7280;
      text-align: center;
      width: 48px;
    }

    /* 對戰隊伍區 */
    .matchup {
      display: flex;
      align-items: center;
      gap: 20px;
    }

    .team {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 4px;
      min-width: 70px;
    }

    .team-badge {
      font-size: 22px;
      font-weight: 900;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .team-record {
      font-size: 12px;
      color: #6b7280;
    }

    .vs-text {
      font-weight: 800;
      color: #9ca3af;
      font-size: 14px;
    }

    /* 隊伍專屬色系代表標記 */
    .dragons { color: #dc2626; }
    .lions { color: #ea580c; }
    .brothers { color: #eab308; }
    .guardians { color: #2563eb; }
    .hawks { color: #059669; }
    .monkeys { color: #831843; }

    /* 球場與時間 */
    .venue-time {
      display: flex;
      flex-direction: column;
      text-align: center;
    }

    .venue-name {
      font-weight: 700;
      font-size: 15px;
      letter-spacing: 2px;
      color: #374151;
    }

    .game-time {
      font-size: 24px;
      font-weight: 900;
      color: #111827;
    }

    /* 天氣預報 */
    .weather-info {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 4px;
      color: #4b5563;
      font-size: 12px;
    }

    .weather-icon {
      font-size: 24px;
      color: #9ca3af;
    }

    /* 先發投手 */
    .pitchers {
      display: flex;
      gap: 12px;
    }

    .pitcher-col {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }

    .pitcher-tag {
      background-color: #1e3a5f;
      color: #ffffff;
      font-size: 11px;
      font-weight: 600;
      padding: 3px 6px;
      border-radius: 2px;
      text-align: center;
    }

    .pitcher-name {
      font-size: 13px;
      font-weight: 700;
      color: #1f2937;
      text-align: center;
    }

    /* 動作按鈕 */
    .actions {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .action-btn {
      background-color: #ffffff;
      border: 1px solid #d1d5db;
      border-radius: 4px;
      padding: 6px 8px;
      font-size: 12px;
      font-weight: 600;
      color: #374151;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      transition: all 0.2s;
    }

    .action-btn:hover {
      background-color: #f9fafb;
      border-color: #9ca3af;
    }

    /* 響應式調整（手機瀏覽適應） */
    @media (max-width: 850px) {
      .game-card {
        grid-template-columns: 1fr;
        gap: 14px;
        text-align: center;
      }
      .matchup, .pitchers, .actions {
        justify-content: center;
      }
      .game-id {
        margin: 0 auto;
      }
    }
  </style>
</head>
<body>

  <!-- 頂部選單 -->
  <header>
    <div class="nav-container">
      <div class="brand">
        <i class="fa-solid fa-baseball-bat-ball"></i> CPBL
      </div>
      <ul class="nav-menu">
        <li><a href="#">最新消息</a></li>
        <li><a href="#" class="active">賽程</a></li>
        <li><a href="#">成績看板</a></li>
        <li><a href="#">球隊戰績</a></li>
        <li><a href="#">數據統計</a></li>
        <li><a href="#">聯盟商城</a></li>
      </ul>
    </div>
  </header>

  <!-- 主內容區 -->
  <main class="container">
    
    <!-- 頂端控制區 -->
    <div class="controls-bar">
      <div class="date-selector">
        <button class="date-btn"><i class="fa-solid fa-chevron-left"></i></button>
        <span id="current-date">2026/10/03 星期六</span>
        <button class="date-btn"><i class="fa-solid fa-chevron-right"></i></button>
      </div>

      <div class="toggle-group">
        <button class="toggle-btn active">一軍</button>
        <button class="toggle-btn">二軍</button>
      </div>
    </div>

    <!-- 賽程卡片 -->
    <div class="games-list">

      <!-- 場次 199 -->
      <div class="game-card">
        <div class="game-id">199</div>
        <div class="matchup">
          <div class="team">
            <span class="team-badge dragons"><i class="fa-solid fa-dragon"></i> 味全</span>
            <span class="team-record">27-31-0</span>
          </div>
          <span class="vs-text">VS.</span>
          <div class="team">
            <span class="team-badge lions"><i class="fa-solid fa-shield-halved"></i> 統一</span>
            <span class="team-record">32-26-0</span>
          </div>
        </div>
        <div class="venue-time">
          <div class="venue-name">亞 太 主</div>
          <div class="game-time">17:05</div>
        </div>
        <div class="weather-info">
          <i class="fa-solid fa-sun weather-icon"></i>
          <span>攝氏31至33度</span>
          <span>降雨機率20%</span>
        </div>
        <div class="pitchers">
          <div class="pitcher-col">
            <div class="pitcher-tag">客場先發</div>
            <div class="pitcher-name">魔神龍</div>
          </div>
          <div class="pitcher-col">
            <div class="pitcher-tag">主場先發</div>
            <div class="pitcher-name">布雷克</div>
          </div>
        </div>
        <div class="actions">
          <button class="action-btn"><i class="fa-solid fa-ticket"></i> 售票資訊</button>
          <button class="action-btn"><i class="fa-solid fa-circle-info"></i> 更多資訊</button>
        </div>
      </div>

      <!-- 場次 200 -->
      <div class="game-card">
        <div class="game-id">200</div>
        <div class="matchup">
          <div class="team">
            <span class="team-badge brothers"><i class="fa-solid fa-crown"></i> 兄弟</span>
            <span class="team-record">34-24-0</span>
          </div>
          <span class="vs-text">VS.</span>
          <div class="team">
            <span class="team-badge guardians"><i class="fa-solid fa-shield-cat"></i> 富邦</span>
            <span class="team-record">24-33-0</span>
          </div>
        </div>
        <div class="venue-time">
          <div class="venue-name">新 莊</div>
          <div class="game-time">17:05</div>
        </div>
        <div class="weather-info">
          <i class="fa-solid fa-cloud weather-icon"></i>
          <span>攝氏28至30度</span>
          <span>降雨機率20%</span>
        </div>
        <div class="pitchers">
          <div class="pitcher-col">
            <div class="pitcher-tag">客場先發</div>
            <div class="pitcher-name">菲力士</div>
          </div>
          <div class="pitcher-col">
            <div class="pitcher-tag">主場先發</div>
            <div class="pitcher-name">瑪帝斯</div>
          </div>
        </div>
        <div class="actions">
          <button class="action-btn"><i class="fa-solid fa-ticket"></i> 售票資訊</button>
          <button class="action-btn"><i class="fa-solid fa-circle-info"></i> 更多資訊</button>
        </div>
      </div>

      <!-- 場次 201 -->
      <div class="game-card">
        <div class="game-id">201</div>
        <div class="matchup">
          <div class="team">
            <span class="team-badge hawks"><i class="fa-solid fa-feather"></i> 台鋼</span>
            <span class="team-record">24-34-0</span>
          </div>
          <span class="vs-text">VS.</span>
          <div class="team">
            <span class="team-badge monkeys"><i class="fa-solid fa-gem"></i> 樂天</span>
            <span class="team-record">32-25-0</span>
          </div>
        </div>
        <div class="venue-time">
          <div class="venue-name">樂天桃園</div>
          <div class="game-time">17:05</div>
        </div>
        <div class="weather-info">
          <i class="fa-solid fa-cloud weather-icon"></i>
          <span>攝氏28至30度</span>
          <span>降雨機率20%</span>
        </div>
        <div class="pitchers">
          <div class="pitcher-col">
            <div class="pitcher-tag">客場先發</div>
            <div class="pitcher-name">坎南</div>
          </div>
          <div class="pitcher-col">
            <div class="pitcher-tag">主場先發</div>
            <div class="pitcher-name">林子崴</div>
          </div>
        </div>
        <div class="actions">
          <button class="action-btn"><i class="fa-solid fa-ticket"></i> 售票資訊</button>
          <button class="action-btn"><i class="fa-solid fa-circle-info"></i> 更多資訊</button>
        </div>
      </div>

    </div>
  </main>

</body>
</html>
