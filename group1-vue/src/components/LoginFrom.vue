<template>
  <div class="login-container">
    <h2>ログイン</h2>

    <form @submit.prevent="handleLogin">
      <!-- メールアドレス入力 -->
      <div class="form-group">
        <label for="email">メールアドレス</label>
        <input type="email" id="email" v-model="email" placeholder="example@mail.com" required />
      </div>

      <!-- パスワード入力 -->
      <div class="form-group">
        <label for="password">パスワード</label>
        <input type="password" id="password" v-model="password" placeholder="パスワードを入力" required />
      </div>

      <!-- ログインボタン -->
      <button type="submit" class="login-btn">ログイン</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// 入力値を保持する変数
const email = ref('');
const password = ref('');

// ログインボタンを押したときの処理
const handleLogin = () => {
  // 本来はここにバックエンド（サーバー）への送信処理を書きます
  console.log('入力されたメール:', email.value);
  console.log('入力されたパスワード:', password.value);

  alert(`ログイン要求を送信しました！\nEmail: ${email.value}`);
};
</script>

<style scoped>
.login-container {
  max-width: 400px;
  margin: 50px auto;
  padding: 30px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 20px;
  text-align: left;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.form-group input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.login-btn {
  width: 100%;
  padding: 12px;
  background-color: #42b883; /* Vueカラー */
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
}

.login-btn:hover {
  background-color: #33a06f;
}
</style>
