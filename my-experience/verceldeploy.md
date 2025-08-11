# vercel部署前端网站

## 在 Vercel 部署网站

假设你的代码已经在 GitHub 上,部署很简单：
	
1.登录 Vercel

https://vercel.com → 用 GitHub 账号登录

2.导入 GitHub 项目

- 点击 “Add New Project”
- 选择 resume-to-web 仓库
- Vercel 会自动检测项目，不需要改设置
- 点击 “Deploy” 等待几秒

  
3. 访问临时域名
部署完成后，Vercel 会分配一个临时域名，例如：https://resume-to-web.vercel.app



## 在 Vercel 绑定域名

可以直接用 Vercel 管理域名，也可以把域名交给 Cloudflare 管理再解析到 Vercel。

### 方法 A：直接在 Vercel 管理域名

	1.	在 Vercel 项目 → Settings → Domains → 添加你自己的域名
	2.	Vercel 会提示你在域名 DNS 里添加两条 CNAME（如果域名是在 Namecheap / 阿里云等购买，就去那边的 DNS 里加）
	3.	等解析生效后，你的域名就会直接指向 Vercel



### 方法 B：在 Cloudflare 管理域名 + 解析到 Vercel（推荐）

如果想用 Cloudflare 做 CDN、SSL、防护等，可以这样做：

步骤 1：把域名接入 Cloudflare

- 登录 https://dash.cloudflare.com
- Add a site → 输入域名
- 选择免费计划（Free Plan）
- Cloudflare 会给你两条新的 NS 记录（nameservers）
- 去域名注册商（阿里云、Namecheap 等）把 NS 服务器改成 Cloudflare 提供的

步骤 2：在 Cloudflare DNS 里解析到 Vercel
- 在 Cloudflare 的 DNS 设置里添加：
- 类型：CNAME
- 名称：@
- 目标：cname.vercel-dns.com
- 代理状态：可以先关闭（灰色云），确保 SSL 配置正常后再开启（橙色云）


如果想 www.域名.com 也能访问，再加一个：
- 类型：CNAME
- 名称：www
- 目标：cname.vercel-dns.com

步骤 3：在 Vercel 绑定域名
- 回到 Vercel → Settings → Domains → 添加域名
- Vercel 会自动检测到 Cloudflare DNS 指向它
- 配置完成后就可以用域名访问网站
