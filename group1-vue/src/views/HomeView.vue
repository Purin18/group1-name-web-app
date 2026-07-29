<template>
  <div class="top-container">
    <!-- ① ヘッダーエリア -->
    <header class="header">
      <div class="header-logo">
        <h1 class="title">Campus Life</h1>
      </div>
    </header>

    <!-- ② メインコンテンツエリア -->
    <main class="main-content">
      <div class="schedule-card">
        <!-- 本日の予定（左側） -->
        <div class="today-section">
          <h2>本日の予定</h2>
          <ul class="list">
            <li>1限から学校</li>
            <li>バイトあり</li>
            <li></li>
            <li></li>
            <li></li>
          </ul>
        </div>

        <!-- 課題（右側に入れ子で配置） -->
        <div class="task-card">
          <h2 class="task-title">課題</h2>
          <ul class="list">
            <li>アプリ</li>
            <li>数学</li>
            <li></li>
            <li></li>
          </ul>
        </div>
      </div>

      <!-- ③ メイン機能ボタン（3列） -->
      <div class="action-buttons">
        <button class="btn main-btn" @click="goToChat">チャット</button>
        <button class="btn main-btn">マッチング</button>
        <button class="btn main-btn">グループ作成</button>
      </div>

      <!-- ④ 最下部ボタン -->
      <div class="footer-button">
        <button class="btn bug-report-btn">不具合報告</button>
      </div>
    </main>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const goToChat = () => {
  router.push('/chat');
};
</script>

<style scoped>
/* 全体のベースカラーとレイアウト */
.top-container {
  min-height: 100vh;
  background-color: #fdf5e6; /* 背景のクリーム色 */
  font-family: sans-serif;
  box-sizing: border-box;
}

/* ヘッダーデザイン */
.header {
  background-color: #ffb6c1; /* ピンク色のヘッダー */
  padding: 15px 30px;
  border-bottom: 2px solid #000;
}

.header-logo {
  display: flex;
  align-items: center;
  gap: 15px;
}

.title {
  margin: 0;
  font-family: 'Georgia', serif;
  font-size: 2.2rem;
  font-weight: normal;
}

.character-placeholder {
  font-size: 2rem;
}

/* メインコンテンツのデザイン */
.main-content {
  max-width: 900px;
  margin: 0 auto;
  padding: 30px 20px;
}

/* 本日の予定＆課題のカード */
.schedule-card {
  background-color: #e6dad0; /* カードのベージュ色 */
  padding: 30px;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 40px;
}

.today-section {
  flex: 1;
}

.today-section h2 {
  font-size: 1.8rem;
  margin-top: 0;
  margin-bottom: 20px;
}

/* 課題エリア */
.task-card {
  flex: 1;
  background-color: #fcfbe3; /* 課題カードの薄黄色 */
  padding: 20px;
  border-radius: 4px;
}

.task-title {
  color: #ff4500; /* 課題の赤文字 */
  font-size: 1.5rem;
  margin-top: 0;
  margin-bottom: 15px;
}

/* リスト共通 */
.list {
  list-style: none;
  padding-left: 0;
  margin: 0;
}

.list li {
  font-size: 1.3rem;
  margin-bottom: 10px;
  min-height: 1.5em; /* 空欄行の高さ確保 */
}

.list li::before {
  content: '・ ';
}

/* ボタン共通 */
.btn {
  cursor: pointer;
  border: 2px solid #000;
  font-size: 1.2rem;
  font-weight: bold;
  transition: opacity 0.2s;
}

.btn:hover {
  opacity: 0.8;
}

/* メインのアクションボタン3個 */
.action-buttons {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 40px;
}

.main-btn {
  flex: 1;
  background-color: #ff6b6b; /* 赤ピンク色のボタン */
  color: #000;
  padding: 15px;
}

/* 不具合報告ボタン */
.footer-button {
  text-align: center;
}

.bug-report-btn {
  background-color: #c8b6ff; /* 薄紫色のボタン */
  color: #000;
  padding: 8px 40px;
  font-size: 0.9rem;
}
</style>
