# 🐒 Puppet Monkey VR - 木偶小猴子交互

基于 [XR Blocks](https://xrblocks.github.io/) 的 WebXR 手势追踪木偶猴子交互体验。

## Pico 4 测试部署

### 方式一：GitHub Pages（推荐）

1. 在 GitHub 上创建新仓库（如 `puppetwebvr`）
2. 将 `index.html` 推送到仓库
3. 进入仓库 Settings → Pages → Source 选择 `main` 分支
4. 等待部署完成后，用 Pico 4 浏览器访问：
   ```
   https://你的用户名.github.io/puppetwebvr/
   ```

### 方式二：本地服务器

```bash
# 使用 Python
python3 -m http.server 8000

# 或使用 Node.js
npx serve .
```

然后在同一局域网的设备上访问 `http://你的IP:8000`

## 修复记录

原代码在 Pico 4 上无法进入 VR，原因有三：

| 问题 | 原因 | 修复 |
|------|------|------|
| 无 "Enter VR" 按钮 | `enableXRTransitions()` 被注释掉 | 重新启用 |
| session 模式不匹配 | 默认 `immersive-ar`，Pico 4 只支持 `immersive-vr` | 添加 `options.enableVR()` |
| hand-tracking 导致 session 失败 | xrblocks 将 `hand-tracking` 作为 `requiredFeature`，Pico 4 可能不支持 | 拦截 `requestSession` 将其降级为 `optionalFeature` |
