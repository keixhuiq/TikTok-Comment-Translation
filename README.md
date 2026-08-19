# TikTok Comment Translation

为 TikTok 网页版评论添加翻译按钮，并支持直播间聊天自动翻译。Chrome / Edge Manifest V3 浏览器扩展。

基于 [DuckCIT/TikTok-Comment-Translator](https://github.com/DuckCIT/TikTok-Comment-Translator) 修改，新增多翻译引擎、直播间翻译和连接测试等功能。

## 功能

- **评论一键翻译**：每条评论旁显示翻译按钮，点击查看译文，再次点击恢复原文
- **直播间聊天自动翻译**：默认关闭，可在弹窗或直播间内开启；译文以附加小字显示在原文下方，不修改原文
- **8 种目标语言**：中文、English、日本語、한국어、Tiếng Việt、Русский、Español、Français

## 翻译服务商

| 服务商 | 说明 |
| --- | --- |
| Google 翻译 | 免费，无需配置 |
| Gemini | 需自填 API Key（在 aistudio.google.com/apikey 获取），默认模型 `gemini-2.5-flash` |
| OpenAI 兼容 | 自填 Endpoint / Model / API Key，支持 OpenAI 官方、DeepSeek、OpenRouter、自部署 vLLM / Ollama 等所有 OpenAI 协议端点 |
| Anthropic Claude | 需自填 API Key（在 console.anthropic.com 获取），默认模型 `claude-haiku-4-5-20251001` |

## 安装

1. 打开 `chrome://extensions/`（或 Edge 扩展页），右上角开启「开发者模式」
2. 点击「加载已解压的扩展程序」，选择本文件夹

更新：用新版本覆盖旧目录后，在扩展页点击刷新图标即可。

## 使用

1. 点击扩展图标打开弹窗，选择目标语言和翻译服务商
2. LLM 服务商需填写 API Key（模型名可留空用默认值），点「测试连接」验证配置
3. 打开 TikTok 视频页，点击评论旁的翻译按钮查看译文
4. 需要直播翻译时，在弹窗打开「直播间评论翻译」开关（默认关闭，持续翻译会产生 API 调用，注意用量）；直播间内也有临时开关可随时暂停

## 注意事项

- API Key 仅保存在当前浏览器本地（`chrome.storage.local`），不会同步到其他设备
- 自定义 OpenAI 兼容 Endpoint 在首次点击「测试连接」时，浏览器会请求该域名的访问权限
- 切换设置无需刷新页面，实时生效
- LLM 翻译失败时可开启「自动降级到 Google 翻译」开关

## 隐私

- 不收集任何数据
- API Key 只保存在本地，不会发送给除所选翻译服务外的任何服务

## 文件结构

```
manifest.json        # 扩展清单 (Manifest V3)
providers.js         # 翻译服务商抽象层
background.js        # 跨域翻译请求与错误处理
content.js           # 评论区翻译按钮
live.js              # 直播间批量自动翻译
content.css          # 页面注入样式
popup/               # 扩展弹窗（设置界面）
data/languages.json  # 多语言 UI 文案
```

## 许可
