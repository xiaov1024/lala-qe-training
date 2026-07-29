# M13 真·完整 GitHub Pages 部署 + OpenMAIC 真·集成(2026-07-29)

> v 真·要厚内容,LALA 补 M13:真·部署 + OpenMAIC 集成
> 真·可执行,v 后期直接用

## 1. GitHub Pages 真·部署

### 1.1 准备仓库
```bash
# 1. 在 Desktop 创建真·部署目录
mkdir -p ~/Desktop/QE-training-site
cd ~/Desktop/QE-training-site

# 2. 复制 LALA 8 大模块
cp -r /Users/v/Desktop/QE培训软件-v0/05-v1真完整/*.md .

# 3. 复制静态网站
cp /Users/v/Desktop/QE培训软件-v0/04-网站/index-v1.html index.html

# 4. 复制图片资源
mkdir -p assets
cp /Users/v/Desktop/QE培训软件-v0/04-网站/*.png assets/

# 5. 创建 README.md
cat > README.md << 'EOF'
# 机加工 + 质量 双技能培训软件 v1
基于 17 份精读 + kaka 8 份报告 + 1910 B 站视频
EOF

# 6. git init + commit
git init
git add .
git commit -m "v1 真·完整"
git branch -M main
```

### 1.2 推到 GitHub
```bash
# 选项 A:gh CLI
gh repo create QE-training-site --public --source=. --remote=origin --push

# 选项 B:手动
# 1. 在 GitHub 上创建 repo (public, no README/LICENSE/.gitignore)
# 2. 复制 repo URL
git remote add origin https://github.com/[v-username]/QE-training-site.git
git push -u origin main
```

### 1.3 启用 GitHub Pages
1. GitHub → repo → Settings → Pages
2. Source: Deploy from a branch
3. Branch: main / (root)
4. Save
5. 访问:`https://[v-username].github.io/QE-training-site/`

### 1.4 自定义域名(可选)
1. 买域名(阿里云 / Cloudflare)
2. DNS:CNAME → `[v-username].github.io`
3. GitHub Pages Settings → Custom domain: `qe.example.com`
4. 启用 HTTPS

## 2. mkdocs-material 部署(更专业)

### 2.1 安装
```bash
pip install mkdocs mkdocs-material
```

### 2.2 配置文件 mkdocs.yml
```yaml
site_name: 机加工 + 质量 双技能培训
site_description: 17 份精读 + kaka 8 份报告 + 1910 B 站视频
site_author: v

theme:
  name: material
  features:
    - navigation.instant
    - navigation.tracking
    - search.suggest
    - content.code.copy
  palette:
    - scheme: default
      primary: indigo
    - scheme: slate
      primary: indigo

nav:
  - 首页: index.md
  - M1 机加工基础: M1-机加工基础-真完整.md
  - M2 SPC + 8 判异规则: M2-SPC-8判异规则-真完整.md
  - M3 FMEA AP 矩阵: M3-FMEA-AP矩阵-真完整.md
  - M4 APQP + PPAP: M4-APQP-PPAP-真完整.md
  - M5 MSA + GR&R: M5-MSA-GRR-真完整.md
  - M6 质量合规 + OEM CSR: M6-质量合规-OEM-CSR-真完整.md
  - M7 老师傅经验外化: M7-老师傅经验外化-真完整.md
  - M8 双技能成长路径: M8-双技能成长路径-真完整.md
  - M9 老师傅访谈 + 奇葩案例: M9-老师傅访谈+学生练习+奇葩案例-真完整.md
  - M10 机加工工艺手册: M10-机加工工艺手册-真完整.md
  - M11 质量工具实战: M11-质量工具实战手册-真完整.md
  - M12 数据 + 薪酬 + 市场: M12-数据+薪酬+市场-真完整.md
```

### 2.3 部署
```bash
mkdocs gh-deploy
# 自动 build + push gh-pages 分支
```

## 3. OpenMAIC 真·集成(3 步)

### 3.1 步骤 1:部署 OpenMAIC(本地)
```bash
# 1. 装 Node.js 20+ pnpm 10+
node -v  # v20+
pnpm -v  # v10+

# 2. clone
git clone https://github.com/THU-MAIC/OpenMAIC.git
cd OpenMAIC
pnpm install

# 3. 启动
pnpm dev
# 浏览器 http://localhost:3000
```

### 3.2 步骤 2:输入 v 试水课题
**打开浏览器** → 输入:
```
课题: 机加工 + 质量 SPC 8 判异
目标用户: 机械/数控 大专学生
课时: 45 分钟
结构: 8 小节 × 5 分钟 + 10 分钟互动
特殊要求: 基于 17 份 AIAG SPC + Western Electric 1956
```

### 3.3 步骤 3:每天 6-10 个变体
**每天流程**:
1. 上午 8:00 - 打开 OpenMAIC
2. 输入当日主题(从 5 大试水课题里选)
3. 生成 6-10 个变体(调整目标用户 + 课时 + 行业)
4. 每天 1 个真·奇葩案例(从 B 站 1910 视频)
5. 下午 - 学生自学
6. 晚上 - 答疑 + 统计

## 4. 真·内容生产模板

### 4.1 试水课题模板
```
课题名: [主题]
目标用户: [用户角色]
课时: [分钟]
前置知识: [需要的]
结构:
  - [小节 1]
  - [小节 2]
  - ...
互动:
  - [问答 1]
  - [问答 2]
真·案例: [真·工厂案例]
参考: [17 份精读里的文件]
```

### 4.2 真·案例库模板
```
案例名: [案例]
背景: [工厂 / 工序 / 批量]
事故: [发生了什么]
损失: [钱/数量/客户]
根因: [5Why + 鱼骨]
解决: [临时 + 永久 + 标准化]
预防: [FMEA 更新 + CP 更新 + 培训]
教训: [3 句话]
```

### 4.3 真·评估模板
```
学生评估:
  - 课堂完成率 %
  - 测验得分 /100
  - 实操评估

老师评估:
  - 内容质量
  - 实战对接
  - 学生反馈

商业评估:
  - 日活 DAU
  - 内容生产
  - 复用率
```

## 5. 真·推广策略(给 v 学生 / 工厂)

### 5.1 B 站真·推广
- 发 1 期视频:"机加工 → 质量工程师 真实路径"
- 内容:小王画像 + 5 阶段 + 双技能溢价
- 标签:#机械 #质量 #SPC #机加工 #FMEA
- 时长:5-8 分钟
- 关联:LALA 8 大模块 PDF 下载链接

### 5.2 知乎真·推广
- 写 1 个长文:"我是怎么从机加工学生变成 PQE 的"
- 关联:链接到 LALA 8 大模块
- 字数:3000-5000

### 5.3 微信真·推广
- 群发:机加工学生群 + 质量工程师群
- 文章:LALA M8 双技能成长路径
- PDF:8 大模块 PDF

### 5.4 工厂真·推广
- 谈 1 个工厂:机加工 PQE 培训
- 课程:LALA M1-M11
- 价格:3-5 万 / 月(咨询式)
- 案例:基于 17 份精读 + 老师傅访谈

## 6. 真·SEO / 流量

### 6.1 B 站真·SEO
- 标题:"机加工 + 质量 双技能 真实路径"
- 标签:机加工 / 质量工程师 / SPC / FMEA / 双技能
- 描述:大专机械 → PQE → 主管 真实路径
- 封面:小王画像 + 双技能对比

### 6.2 知乎真·SEO
- 标题:"机加工 + 质量 双技能 怎么转"
- 标签:机械 / 质量 / 求职 / 双技能
- 内容:真实数据 + 17 份精读引用
- 评论:持续互动

### 6.3 真·SEO 关键词
- 机加工 + 质量
- SPC 8 判异规则
- FMEA AP 矩阵
- 双技能
- 机加工 PQE
- 质量工程师薪资
- 机加工 SPC
- 工厂质量部

## 7. 真·商业模式(给 v 参考)

### 7.1 内容 + 工具
- **免费**:8 大模块 PDF + 静态网站
- **付费**:OpenMAIC 部署 + 老师傅访谈 + 工厂咨询
- **预计**:3-5 万 / 工厂 / 月

### 7.2 内容 + 培训
- **免费**:B 站 / 知乎内容
- **付费**:群(99 元/月)+ 1 对 1(500 元/小时)
- **预计**:5-10 万 / 年

### 7.3 内容 + 工厂咨询
- **免费**:案例库
- **付费**:咨询项目(20-50 万 / 项目)
- **预计**:50-100 万 / 年

## 8. 真·时间表(给 v)

### 8.1 1 周(基础)
- 跑 OpenMAIC 试 1 课题
- 静态网站部署
- 1 期 B 站视频

### 8.2 1 月(起步)
- 8 大模块完整
- 每天 1 课题(2-3 变体)
- 1 期 B 站视频
- 知乎 1 篇

### 8.3 3 月(扩张)
- 50+ 课题库
- 1 工厂咨询
- 200+ 学生
- 1 万粉丝(B 站 / 知乎)

### 8.4 6 月(稳定)
- 200+ 课题
- 5 工厂咨询
- 1000+ 学生
- 5 万粉丝
- 月入 5-10 万

## 9. 真·风险

### 9.1 内容风险
- **错**:内容错误 → 多源验证(17 份精读 + kaka)
- **过时**:标准变化 → 季度更新
- **同质**:市场饱和 → 双技能差异

### 9.2 商业风险
- **慢**:客户成长慢 → 2-3 月
- **低**:客户单价低 → 工厂大客户
- **难**:老师傅访谈难 → 提供激励

### 9.3 技术风险
- **OpenMAIC 装不上**:备选 Docker
- **GitHub Pages 限制**:100 GB 带宽
- **CDN 慢**:Cloudflare 免费

## 10. 真·参考资料

- 17 份精读
- kaka v19 GitHub Pages 部署指南
- kaka v13 海外培训资源
- OpenMAIC 官网 + GitHub
- mkdocs-material 文档

---

_LALA 2026-07-29 05:30_
_输入: 17 份精读 + kaka v13/v19 + OpenMAIC 官网_
_输出: M13 真·部署 + OpenMAIC 集成 + 商业模式 + 时间表_
_为 v 真·补厚_