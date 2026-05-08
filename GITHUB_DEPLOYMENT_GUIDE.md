# 📱 GitHub Pages 部署指南 - 泪与息

## 问题排查

你的页面显示空白的原因通常是以下几种：

### ✅ 常见问题及解决方案

| 问题 | 症状 | 解决方案 |
|------|------|--------|
| **文件命名错误** | 访问 repo URL 显示 404 | 确保文件名为 `index.html` |
| **外部资源加载失败** | 页面加载但无内容显示 | 检查 DevTools 看 CDN 资源是否加载成功 |
| **CORS 错误** | 控制台报跨域错误 | 使用 HTTPS CDN（已在优化版本中处理） |
| **安全策略限制** | 脚本不执行 | 添加 CSP meta 标签（已在优化版本中处理） |
| **GitHub Pages 未启用** | 访问显示 404 | 去 Settings → Pages，选择 branch |

---

## 🚀 部署步骤

### 方式一：快速部署（5 分钟）

#### 步骤 1：创建新仓库
```bash
# 在 GitHub 上创建新仓库，名称可以是：
username.github.io              # 个人主页（推荐）
或
tear-healing                    # 项目仓库
```

#### 步骤 2：克隆仓库到本地
```bash
git clone https://github.com/YOUR_USERNAME/tear-healing.git
cd tear-healing
```

#### 步骤 3：上传文件
```bash
# 将 index.html 复制到仓库根目录
cp index.html .

# 添加文件到 Git
git add index.html
git commit -m "Initial commit: Add tear-healing app"
git push -u origin main
```

#### 步骤 4：启用 GitHub Pages
1. 打开你的仓库：`https://github.com/YOUR_USERNAME/tear-healing`
2. 点击 **Settings**
3. 左侧菜单找到 **Pages**
4. 在 "Source" 下选择：**Deploy from a branch**
5. 选择分支：**main** （或 master）
6. 点击 **Save**

#### 步骤 5：等待部署完成
- 通常需要 1-3 分钟
- 完成后会显示访问 URL：`https://YOUR_USERNAME.github.io/tear-healing`

---

### 方式二：使用 gh-pages 分支（可选）

如果你想使用专门的 `gh-pages` 分支：

```bash
# 创建新分支
git checkout -b gh-pages

# 确保 index.html 在根目录
git add index.html
git commit -m "Deploy to gh-pages"

# 推送到 GitHub
git push origin gh-pages
```

然后在 Settings → Pages 中选择 `gh-pages` 分支。

---

## 🔍 测试与调试

### 检查是否正确部署

#### 1. 浏览器测试
```
访问：https://YOUR_USERNAME.github.io/tear-healing
```

#### 2. 打开浏览器控制台查看错误
- **Windows/Linux**: `F12`
- **Mac**: `Cmd + Option + I`
- 查看 **Console** 标签页的红色错误信息

#### 3. 检查网络请求
在 **Network** 标签页查看：
- `index.html` 是否成功加载（状态码 200）
- CDN 资源是否加载：
  - `https://cdn.jsdelivr.net/npm/@mediapipe/...`
  - `https://fonts.googleapis.com/...`

### 常见错误信息

```
❌ "Failed to load script from 'https://cdn.jsdelivr.net/...'"
→ 网络问题，刷新页面或检查 CDN 状态

❌ "camera permission denied"
→ 摄像头权限被拒绝，点击浏览器地址栏的权限图标允许

❌ "Hands is not defined"
→ MediaPipe 库加载失败，等待几秒后刷新页面
```

---

## 📦 文件结构（推荐）

```
tear-healing/
├── index.html           # 主文件（必需）
├── README.md            # 项目说明
├── LICENSE              # 许可证
└── .gitignore           # 忽略文件配置
```

---

## 🎯 确保页面能正常显示的检查清单

- [ ] 文件命名为 `index.html`
- [ ] 已推送到 GitHub 仓库
- [ ] GitHub Pages 已启用（Settings → Pages）
- [ ] 选择了正确的分支（main 或 master）
- [ ] 等待了 1-3 分钟以完成部署
- [ ] 访问 URL 正确：`https://username.github.io/repo-name`
- [ ] 打开浏览器控制台，检查是否有红色错误
- [ ] 允许网页访问摄像头权限
- [ ] 网络连接正常（CDN 可访问）
- [ ] 清除浏览器缓存后重新访问

---

## 🌐 自定义域名（可选）

如果你想使用自己的域名：

1. 在仓库根目录创建 `CNAME` 文件
2. 写入你的域名：`yourdomain.com`
3. 推送到 GitHub
4. 在你的域名注册商配置 DNS 指向 GitHub Pages

```bash
# 创建 CNAME 文件
echo "yourdomain.com" > CNAME
git add CNAME
git commit -m "Add custom domain"
git push
```

---

## 🔐 HTTPS 安全

GitHub Pages 自动提供 HTTPS 证书，你的网站会自动重定向到 HTTPS。

---

## 📞 如果仍然有问题

### 检查清单
- 在浏览器地址栏看到的 URL 是否与仓库 Settings 中显示的 URL 一致？
- 控制台错误信息是什么？
- 刷新页面并清除缓存（Ctrl+Shift+Delete）再试一次？

### 获取帮助
1. 查看 [GitHub Pages 官方文档](https://docs.github.com/en/pages)
2. 检查 [MediaPipe CDN 状态](https://cdn.jsdelivr.net/)
3. 查看 [浏览器控制台错误](https://developer.mozilla.org/en-US/docs/Tools/Browser_Console)

---

## 💡 性能优化建议

如果页面加载较慢：

1. **启用 Gzip 压缩**：GitHub Pages 自动启用
2. **使用 CDN**：已使用 jsDelivr CDN
3. **优化图像**：尽量减少大文件
4. **缓存策略**：浏览器会自动缓存资源

---

## 📝 更新网站

每次修改代码后：

```bash
# 编辑 index.html 文件

# 推送更新
git add index.html
git commit -m "Update: description of changes"
git push origin main
```

更新通常在 1-2 分钟内生效。

---

**祝你部署成功！🎉**

如有问题，请检查浏览器控制台（F12）的错误信息。
