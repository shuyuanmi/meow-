// ==UserScript==
// @name         喵喵套件 Loader
// @namespace    meow-pencil-suite
// @version      1.0
// @description  从 GitHub 加载喵喵套件（核心 + 小手机）
// @match        *://*/*
// @grant        none
// @run-at       document-idle
// ==/UserScript==

(function() {
  'use strict';

  // ===== ✏️ 在这里填你的 GitHub Raw 地址 =====
  // 格式：https://raw.githubusercontent.com/你的用户名/你的仓库名/main/文件名.js
  const PLUGINS = [
    'https://raw.githubusercontent.com/shuyuanmi/meow-/main/meow-core.js',
    'https://raw.githubusercontent.com/shuyuanmi/meow-/main/meow-phone.js',
  ];
  // ============================================

  // 顺序加载：core 必须在 phone 之前
  function loadScript(url) {
    return new Promise((resolve, reject) => {
      const s = document.createElement('script');
      s.src = url + '?t=' + Date.now();  // 防缓存
      s.onload = () => {
        console.log('[MEOW Loader] ✓ 已加载:', url.split('/').pop().split('?')[0]);
        resolve();
      };
      s.onerror = () => {
        console.error('[MEOW Loader] ✗ 加载失败:', url);
        reject(new Error('加载失败: ' + url));
      };
      (document.head || document.documentElement).appendChild(s);
    });
  }

  async function boot() {
    for (const url of PLUGINS) {
      try {
        await loadScript(url);
      } catch(e) {
        console.error('[MEOW Loader]', e);
        // core 加载失败就不继续了
        if (url.includes('core')) break;
      }
    }
  }

  boot();
})();
