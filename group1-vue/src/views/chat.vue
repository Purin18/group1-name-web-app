<script setup>
import { ref, nextTick } from 'vue';

// --- 画面切り替え用の状態 ---
// nullのときは選択画面、データが入るとチャット画面になります
const selectedMember = ref(null);
import { useRouter } from 'vue-router';

const router = useRouter();

// ホーム画面に戻る処理
const goHome = () => {
  router.push('/'); // ホームのパス（'/'）へ移動
};
// メンバー一覧データ
const members = [
  { id: 1, name: '「武庫川」さん' }, // 一番上（移行可能）
  { id: 2, name: '「文月」さん' }, // 移行しない（設定なし）
  { id: 3, name: '「ラビー」さん' } // 移行しない（設定なし）
];

// メンバー選択時の処理
const selectMember = (index, member) => {
  if (index === 0) {
    // 一番上（index === 0）のときだけチャット画面へ遷移
    selectedMember.value = member;
  }
};

// 選択画面に戻る処理
const goBack = () => {
  selectedMember.value = null;
};

// --- チャット履歴のデータ（配列） ---
const messages = ref([
  { id: 1, text: '初めましてかな？私は情報の「武庫川」です！', sender: 'other', time: '10:00' },
  { id: 2, text: '初めまして！私は、大日の「西宮」です！', sender: 'user', time: '10:01' }
]);

// 入力フォームのテキスト
const newMessage = ref('');

// スクロール制御用の要素参照
const chatContainer = ref(null);

// メッセージ送信処理
const sendMessage = async () => {
  if (!newMessage.value.trim()) return;

  const now = new Date();
  const timeString = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });

  messages.value.push({
    id: Date.now(),
    text: newMessage.value,
    sender: 'user',
    time: timeString
  });

  newMessage.value = '';

  await scrollToBottom();

  setTimeout(async () => {
    messages.value.push({
      id: Date.now(),
      text: `私も！同じ推しの人と話せてうれしいな！`,
      sender: 'other',
      time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    });
    await scrollToBottom();
  }, 1000);
};

// スクロール処理
const scrollToBottom = async () => {
  await nextTick();
  if (chatContainer.value) {
    chatContainer.value.scrollTop = chatContainer.value.scrollHeight;
  }
};
</script>

<template>
  <!-- 【画面1】メンバー選択画面（selectedMember が null の時に表示） -->
  <div v-if="!selectedMember" class="chat-container">
    <header class="chat-header">
      <button class="back-btn" @click="goHome">← 戻る</button>
      <h2>メンバー選択</h2>
    </header>

    <div class="member-list">
      <button
        v-for="(member, index) in members"
        :key="member.id"
        class="member-card"
        @click="selectMember(index, member)"
      >
        <span class="name">{{ member.name }}</span>
      </button>
    </div>
  </div>

  <!-- 【画面2】チャット画面（selectedMember に値が入った時に表示） -->
  <div v-else class="chat-container">
    <!-- ヘッダー（戻るボタン付き） -->
    <header class="chat-header chat-header-with-back">
      <button @click="goBack" class="back-btn">← 戻る</button>
      <h2>チームチャット</h2>
    </header>

    <!-- メッセージ一覧エリア -->
    <div class="message-list" ref="chatContainer">
      <div
        v-for="msg in messages"
        :key="msg.id"
        :class="['message-item', msg.sender === 'user' ? 'message-self' : 'message-other']"
      >
        <div class="bubble">
          <p class="text">{{ msg.text }}</p>
          <span class="time">{{ msg.time }}</span>
        </div>
      </div>
    </div>

    <!-- 入力フォーム -->
    <form @submit.prevent="sendMessage" class="input-area">
      <input v-model="newMessage" type="text" placeholder="メッセージを入力..." class="chat-input" />
      <button type="submit" class="send-btn">送信</button>
    </form>
  </div>
</template>

<style scoped>
/* 全体レイアウト */
.chat-container {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 450px;
  height: 600px;
  margin: 20px auto;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  background-color: #f7f9fa;
  font-family: sans-serif;
  overflow: hidden;
}

/* ヘッダー */
.chat-header {
  background-color: #ffb6c1;
  color: white;
  padding: 16px;
  text-align: center;
  position: relative;
}
.chat-header h2 {
  margin: 0;
  font-size: 1.1rem;
}

.chat-header-with-back {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* 戻るボタン */
.back-btn {
  position: absolute;
  left: 12px;
  background: transparent;
  border: none;
  color: white;
  font-size: 0.9rem;
  font-weight: bold;
  cursor: pointer;
}

/* メンバー選択画面のスタイル */
.member-list {
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.member-card {
  display: flex;
  align-items: center;
  padding: 16px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background-color: #ffffff;
  cursor: pointer;
  font-size: 1rem;
  color: #333;
  width: 100%;
  box-sizing: border-box;
}

.member-card:hover {
  border-color: #ffb6c1;
}

/* メッセージエリア */
.message-list {
  flex: 1;
  padding: 16px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.message-item {
  display: flex;
  width: 100%;
}

/* 自分（右側） */
.message-self {
  justify-content: flex-end;
}
.message-self .bubble {
  background-color: #ffb6c1;
  color: white;
  border-bottom-right-radius: 2px;
}
.message-self .time {
  color: rgba(255, 255, 255, 0.8);
}

/* 相手（左側） */
.message-other {
  justify-content: flex-start;
}
.message-other .bubble {
  background-color: #ffffff;
  color: #333;
  border-bottom-left-radius: 2px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}
.message-other .time {
  color: #888;
}

/* 吹き出しスタイル */
.bubble {
  max-width: 75%;
  padding: 10px 14px;
  border-radius: 16px;
  word-break: break-word;
}
.text {
  margin: 0 0 4px 0;
  font-size: 0.95rem;
  line-height: 1.4;
}
.time {
  font-size: 0.7rem;
  display: block;
  text-align: right;
}

/* 入力欄 */
.input-area {
  display: flex;
  padding: 12px;
  background-color: #fff;
  border-top: 1px solid #e0e0e0;
  gap: 8px;
}
.chat-input {
  flex: 1;
  padding: 10px 14px;
  border: 1px solid #ccc;
  border-radius: 20px;
  outline: none;
  font-size: 0.95rem;
}
.chat-input:focus {
  border-color: #ffb6c1;
}
.send-btn {
  padding: 10px 18px;
  background-color: #ffb6c1;
  color: white;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  font-weight: bold;
}
.send-btn:hover {
  background-color: #ffb6c1;
}
</style>
