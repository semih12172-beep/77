# 🎸 ak77 — LINKIN PARK × 我的空间

一个献给林肯公园的个人主页，移动端优先设计，支持 PWA 安装到手机桌面。

---

## ✨ 功能特性

- **黑胶播放器** — 旋转唱片 + 唱臂动画 + 均衡器跳动
- **双语歌词** — 中英文对照，随播放进度自动高亮滚动
- **歌单管理** — 5首经典曲目，左右滑动切歌
- **拍立得照片墙** — 胶卷风格随机倾斜排列
- **PWA 支持** — iOS/Android 均可添加到主屏幕，像原生 App 体验
- **底部 Tab 导航** — iOS 风格，毛玻璃效果
- **Mini 播放条** — 切换页面时常驻底部，随时控制音乐

## 🛠️ 技术栈

- 纯 HTML / CSS / JavaScript，零依赖，零框架
- CSS 变量 + GPU 加速动画（`will-change`, `translateZ(0)`）
- Safe Area Inset 适配 iPhone 刘海 / 灵动岛 / Home 条
- 触摸手势：滑动切歌、拖拽进度条

---

## 🚀 VPS 部署教程

### 方式一：Nginx 静态托管（推荐）

**1. 在 VPS 上安装 Nginx**
```bash
# Ubuntu / Debian
sudo apt update && sudo apt install -y nginx

# CentOS / Rocky
sudo yum install -y nginx
```

**2. 上传文件到 VPS**
```bash
# 在本机执行，把 index.html 传到服务器
scp index.html root@你的VPS_IP:/var/www/ak77/index.html
```

**3. 配置 Nginx**
```bash
# 创建网站目录
sudo mkdir -p /var/www/ak77

# 创建 Nginx 配置
sudo nano /etc/nginx/sites-available/ak77
```

粘贴以下内容（替换 `你的域名或IP`）：
```nginx
server {
    listen 80;
    server_name 你的域名或IP;

    root /var/www/ak77;
    index index.html;

    # Gzip 压缩
    gzip on;
    gzip_types text/html text/css application/javascript;

    # 缓存静态资源
    location ~* \.(html|css|js)$ {
        add_header Cache-Control "public, max-age=3600";
    }

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

**4. 启用并启动**
```bash
sudo ln -s /etc/nginx/sites-available/ak77 /etc/nginx/sites-enabled/
sudo nginx -t          # 检查配置
sudo systemctl restart nginx
sudo systemctl enable nginx
```

**5. 开放防火墙端口**
```bash
sudo ufw allow 80
sudo ufw allow 443   # 如果要上 HTTPS
```

---

### 方式二：HTTPS + 免费 SSL（可选但推荐）

```bash
# 安装 Certbot
sudo apt install -y certbot python3-certbot-nginx

# 自动申请证书（替换为你的域名）
sudo certbot --nginx -d 你的域名.com

# 自动续期
sudo crontab -e
# 添加这行：
0 3 * * * certbot renew --quiet
```

---

### 方式三：用 GitHub Pages 免费托管（备选）

1. 创建仓库后，进入 **Settings → Pages**
2. Source 选 **Deploy from branch → main → / (root)**
3. 保存后访问 `https://你的用户名.github.io/ak77`

---

## 📁 文件结构

```
ak77/
├── index.html     # 全部代码，单文件部署
└── README.md      # 本文档
```

---

## 📱 手机添加到主屏幕

**iOS (Safari)**：打开页面 → 底部分享按钮 → "添加到主屏幕"

**Android (Chrome)**：打开页面 → 右上角菜单 → "添加到主屏幕"

---

## 🎵 歌曲列表

| # | 曲名 | 专辑 |
|---|------|------|
| 1 | In The End | Hybrid Theory (2000) |
| 2 | Numb | Meteora (2003) |
| 3 | Crawling | Hybrid Theory (2000) |
| 4 | What I've Done | Minutes to Midnight (2007) |
| 5 | Somewhere I Belong | Meteora (2003) |

---

## 💡 自定义说明

- **替换照片**：在 `photos` 数组里将 emoji 换成 `<img>` 标签或图片 URL
- **添加歌曲**：在 `songs` 数组里按格式添加，包含 `title / artist / album / duration / lyrics`
- **修改主题色**：编辑 CSS `:root` 里的 `--red` 变量

---

*Made with ♥ for Linkin Park — Chester, forever in our hearts. 🖤*
