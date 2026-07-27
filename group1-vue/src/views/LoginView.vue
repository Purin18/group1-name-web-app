<!-- src/views/LoginView.vue -->

<template>
  <div class="login-container">
    <!-- ① トップ画面と同じヘッダー -->
    <header class="header">
      <div class="header-logo">
        <h1 class="title">Campus Life</h1>
        <!-- 必要に応じてトップと同じキャラクター画像を表示 -->
        <div class="character-placeholder">🐰</div>
      </div>
    </header>

    <!-- ② メインコンテンツ（中央配置のログインカード） -->
    <main class="main-content">
      <div class="login-card">
        <h2 class="login-title">ログイン</h2>

        <form @submit.prevent="handleLogin">
          <!-- 入力エリア1：メールアドレス -->
          <div class="form-group">
            <label for="email">メールアドレス</label>
            <input type="email" id="email" placeholder="example@mail.com" required />
          </div>

          <!-- 入力エリア2：パスワード -->
          <div class="form-group">
            <label for="password">パスワード</label>
            <input type="password" id="password" placeholder="••••••••" required />
          </div>

          <!-- ③ アクションボタン（トップ画面のボタンと同じデザイン） -->
          <div class="login-action">
            <button type="submit" class="btn login-btn">ログイン</button>
          </div>
        </form>

        <!-- 補助リンク -->
        <div class="helper-links">
          <a href="#" class="link">パスワードを忘れた場合</a>
          <span class="separator">|</span>
          <a href="#" class="link">新規登録（まだの方）</a>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

// ログインボタンを押した時の処理
const handleLogin = () => {
  // まずは認証なしでトップ画面へ遷移させます
  router.push('/');
};
</script>

<style scoped>
/* 全体のベースレイアウト（トップ画面と共通のクリーム背景） */
.login-container {
  min-height: 100vh;
  background-color: #fdf5e6;
  font-family: sans-serif;
  box-sizing: border-box;
}

/* ヘッダーデザイン（トップ画面と完全に共通） */
.header {
  background-color: #ffb6c1; /* ピンク */
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

/* メインコンテンツ（カードを中央に配置） */
.main-content {
  max-width: 900px;
  margin: 0 auto;
  padding: 50px 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* ログインカードのデザイン（トップ画面のベージュカードを参考） */
.login-card {
  background-color: #e6dad0; /* ベージュ */
  padding: 40px;
  border-radius: 4px;
  width: 100%;
  max-width: 450px; /* カードの幅 */
  border: 2px solid #000; /* デザインに合わせた黒枠 */
}

.login-title {
  font-size: 1.8rem;
  margin-top: 0;
  margin-bottom: 30px;
  text-align: center;
}

/* フォームのデザイン */
.form-group {
  margin-bottom: 20px;
  text-align: left;
}

.form-group label {
  display: block;
  font-size: 1.1rem;
  font-weight: bold;
  margin-bottom: 8px;
}

/* 入力欄（Figmaの雰囲気に合わせてシンプルに） */
.form-group input {
  width: 100%;
  padding: 12px;
  font-size: 1.1rem;
  border: 2px solid #000; /* 黒枠 */
  border-radius: 4px;
  background-color: #fff;
  box-sizing: border-box;
}

.form-group input:focus {
  outline: none;
  border-color: #ff6b6b; /* フォーカス時にボタンの色にする */
}

/* アクションボタン（トップ画面の赤ピンクボタンを継承） */
.login-action {
  margin-top: 30px;
  margin-bottom: 20px;
}

.btn {
  width: 100%;
  cursor: pointer;
  border: 2px solid #000;
  font-size: 1.3rem;
  font-weight: bold;
  padding: 15px;
  transition: opacity 0.2s;
}

.btn:hover {
  opacity: 0.8;
}

.login-btn {
  background-color: #ff6b6b; /* トップと同じ赤ピンク色 */
  color: #000;
}

/* 補助リンク */
.helper-links {
  text-align: center;
  font-size: 0.9rem;
  margin-top: 20px;
}

.link {
  color: #000;
  text-decoration: underline;
}

.separator {
  margin: 0 10px;
  color: #666;
}
</style>
