<template>
  <div class="login-page">
    <h2>ログイン</h2>
    <!-- @submit.prevent="handleLogin" でフォーム送信時に handleLogin 関数を実行 -->
    <form @submit.prevent="handleLogin">
      <div class="form-group">
        <label>メールアドレス</label>
        <input type="email" placeholder="example@email.com" required />
      </div>
      <div class="form-group">
        <label>パスワード</label>
        <input type="password" required />
      </div>
      <button type="submit" class="login-btn">ログイン</button>
    </form>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

// ルーターを操作するための設定
const router = useRouter();

// ログインボタンが押された時の処理
const handleLogin = () => {
  // 本来はここでパスワード認証などの処理を行いますが、
  // まずはそのままトップ画面（'/'）へ移動（リダイレクト）させます！
  router.push('/');
};
</script>

<style scoped>
.login-page {
  max-width: 350px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  text-align: center;
}
.form-group {
  margin-bottom: 15px;
  text-align: left;
}
.form-group label {
  display: block;
  margin-bottom: 5px;
}
.form-group input {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}
.login-btn {
  width: 100%;
  padding: 10px;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
</style>
