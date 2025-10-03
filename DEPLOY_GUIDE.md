# Argosbx 在 Leapcell 上的部署指南

## 项目概述

这是一个 Argosbx 配置生成器的静态网站版本，用于生成 Argosbx 一键脚本的 SSH 命令。该项目已经优化，可以直接在 Leapcell 平台上部署。

## 部署准备

### 1. 文件结构
确保您的项目包含以下文件：
```
argosbx/
├── index.html          # 主要的静态网页
├── package.json        # 项目配置文件
├── vercel.json         # 部署配置文件
├── .gitignore          # Git 忽略文件
├── README.md           # 原项目说明
├── argosbx.sh          # 原始脚本（可选）
└── DEPLOY_GUIDE.md     # 本部署指南
```

### 2. 核心文件说明
- **index.html**: 完全自包含的静态网页，包含配置生成器界面
- **package.json**: 项目元数据和依赖配置
- **vercel.json**: 部署配置，包含路由和安全头设置

## 在 Leapcell 上部署

### 方法一：通过 Git 仓库部署（推荐）

1. **准备 Git 仓库**
   ```bash
   # 如果还没有 Git 仓库，初始化一个
   git init
   git add .
   git commit -m "Initial commit for Leapcell deployment"
   
   # 推送到 GitHub/GitLab
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

2. **在 Leapcell 控制台部署**
   - 登录 Leapcell 控制台
   - 选择 "静态网站" 或 "Static Site" 服务
   - 连接您的 Git 仓库
   - 配置部署设置：
     - **Build Command**: `echo "No build required"`
     - **Output Directory**: `./` (根目录)
     - **Install Command**: `npm install` (可选)

3. **配置环境变量**（如果需要）
   - 在 Leapcell 控制台的环境变量页面添加任何必要的配置

### 方法二：手动文件上传

1. **准备文件**
   - 确保所有必要文件都在项目根目录
   - 压缩项目文件为 ZIP 格式

2. **上传部署**
   - 在 Leapcell 控制台选择手动上传
   - 上传 ZIP 文件
   - 等待部署完成

## 部署后配置

### 1. 域名设置
- 在 Leapcell 控制台配置自定义域名
- 更新 `index.html` 中的 `canonical` 链接为您的实际域名
- 如果使用自定义域名，记得配置 SSL 证书

### 2. 性能优化
- 启用 CDN 加速（Leapcell 通常默认启用）
- 配置缓存策略
- 启用 Gzip 压缩

### 3. 安全设置
项目已包含基本的安全头设置在 `vercel.json` 中：
- X-Content-Type-Options: nosniff
- X-Frame-Options: DENY  
- X-XSS-Protection: 1; mode=block
- Referrer-Policy: strict-origin-when-cross-origin

## 验证部署

部署完成后，访问您的网站URL应该能看到：
1. **Argosbx配置生成器界面**
2. **深色/浅色主题切换功能**
3. **各种协议配置选项**
4. **SSH命令生成功能**

## 常见问题

### Q: 网站打开显示 404 错误
**A**: 检查 `vercel.json` 中的路由配置，确保所有请求都指向 `index.html`

### Q: 样式显示异常
**A**: 确保 `index.html` 文件完整，所有 CSS 都内嵌在文件中

### Q: 生成的命令无法执行
**A**: 这是正常的，生成的命令需要在目标服务器上执行，不是在浏览器中执行

### Q: 如何更新网站内容
**A**: 
- 如果使用 Git 部署：修改文件后推送到仓库即可自动重新部署
- 如果手动上传：重新上传更新的文件

## 维护建议

1. **定期更新**: 关注原项目更新，及时同步最新功能
2. **监控访问**: 使用 Leapcell 提供的分析工具监控网站访问情况
3. **备份文件**: 定期备份配置文件和自定义修改
4. **安全检查**: 定期检查安全头设置和SSL证书状态

## 技术支持

- **原项目**: https://github.com/yonggekkk/argosbx
- **Leapcell文档**: 查看 Leapcell 官方文档
- **问题反馈**: 可在原项目仓库提交 Issue

---

**注意**: 本部署指南适用于 Leapcell 平台，其他平台可能需要调整配置文件。