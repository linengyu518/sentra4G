# SENTRA P5 — 官网 + 控制台演示（前端静态站点）

这是 SENTRA P5 随身 4G 相机的**前端**:营销官网 + 用户控制台演示界面,单文件纯静态站点(`index.html`),可直接部署到 GitHub Pages。

- 中英文切换、登录 / 注册 / 找回密码、修改密码
- 控制台:设备管理、收件箱管理(每台最多 3 个)、照片相册(按日期筛选、单张删除、保留 15 天提示)
- 购买页:速卖通 / 亚马逊跳转
- 设备定位:随身携带,**由使用端手动触发拍照并上传**,无定时 / 无计划拍照,microSD 最大 32GB

> ⚠️ 说明:控制台目前是**纯前端演示**,所有数据保存在浏览器内存中,刷新即重置,不连接真实后端。真实的中转服务器 / 接口由后端单独实现(参见此前的《服务器接口与数据库设计》文档),前端接好 API 后即为正式功能。

---

## 目录结构

```
.
├── index.html                 # 站点主文件（GitHub Pages 入口）
├── .nojekyll                  # 关闭 Jekyll 处理，按原样发布静态文件
├── .gitignore
├── README.md
└── .github/
    └── workflows/
        └── deploy.yml         # 自动部署到 GitHub Pages 的工作流
```

---

## 部署方式一:用 GitHub Actions 自动部署(推荐)

本仓库已自带 `.github/workflows/deploy.yml`,推到 GitHub 后会自动部署。

1. 在 GitHub 新建一个仓库(例如 `sentra-site`)。
2. 在本地把这些文件推上去:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: SENTRA P5 site"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/<仓库名>.git
   git push -u origin main
   ```
3. 打开仓库的 **Settings → Pages**,把 **Build and deployment → Source** 选为 **GitHub Actions**。
4. 等 **Actions** 标签里的部署任务跑完(约 1 分钟),页面会显示访问网址,形如:
   `https://<你的用户名>.github.io/<仓库名>/`

之后每次 `git push` 到 `main`,都会自动重新部署。

---

## 部署方式二:从分支直接发布(不用 Actions)

如果不想用工作流,也可以:

1. 同样把文件推到 GitHub 的 `main` 分支(可删除 `.github/` 目录)。
2. **Settings → Pages → Source** 选 **Deploy from a branch**。
3. 分支选 `main`,目录选 `/ (root)`,保存。
4. 稍等片刻,同样会得到 `https://<你的用户名>.github.io/<仓库名>/`。

---

## 绑定自定义域名(可选)

1. 在仓库根目录新增一个名为 `CNAME` 的文件,内容写你的域名,例如:
   ```
   www.sentra-cam.com
   ```
2. 到你的域名服务商处,把该域名 CNAME 解析到 `<你的用户名>.github.io`。
3. 回到 **Settings → Pages** 填入自定义域名并勾选 **Enforce HTTPS**。

---

## 本地预览

任意静态服务器即可,例如:

```bash
# Python
python3 -m http.server 8080
# 然后浏览器打开 http://localhost:8080
```

或直接用浏览器打开 `index.html` 也能看(部分浏览器对本地文件限制较多,建议用上面的本地服务器)。

---

## 待办 / 后续

- [ ] 把购买页里的 `https://www.aliexpress.com` 和 `https://www.amazon.com` 换成真实商品链接
- [ ] 控制台对接真实后端 API(登录、注册、找回密码、设备绑定、收件人、照片列表/删除、改密码)
- [ ] 如需开源/版权声明,自行添加 `LICENSE` 文件
