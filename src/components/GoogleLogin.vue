<script setup>
import { onMounted } from 'vue';
// src/stores/auth.js (或直接在 App.vue 中使用 provide/inject)
import { reactive, computed } from 'vue';

const authState = reactive({
  isGoogleLoggedIn: false,
  isFacebookLoggedIn: false,
  googleProfile: null,
  facebookProfile: null,
  // 必須兩個都登入才能查詢
  canQuery: computed(() => authState.isGoogleLoggedIn),
});

// ... 匯出相關方法和狀態

onMounted(() => {
  // 確保只在瀏覽器環境執行
  if (window.google) {
    window.google.accounts.id.initialize({
      client_id: '737444360335-03fp8kjs1alt73gi9dnr700ki5j12uhc.apps.googleusercontent.com',
      callback: handleGoogleLogin, // 處理登入回調
    });

    window.google.accounts.id.renderButton(
      document.getElementById('google-button-container'),
      { theme: 'outline', size: 'large' }
    );
  }
});

const handleGoogleLogin = (response) => {
 console.log(response, " response");
  authState.isGoogleLoggedIn = true;
  // authState.googleProfile = parseJwt(response.credential);
};
</script>

<template>

  <div id="google-button-container"></div>

  
</template>