# 梅花易数学堂 — 开工工作流

> 🔴 每次开始本项目的开发工作，必须先读取本文档

---

## 第一步：读取状态

```bash
# 读大纲确认当前进度
read_file /home/ubuntu/meihua-pwa/SYLLABUS.md
```

找到「全局状态追踪」段落，确认：
- 当前关卡编号和名称
- 所属单元
- 开工清单

---

## 第二步：古典来源验证 🔴

### 2.1 查阅原文
根据大纲中的「来源」标注，找到古典原文。

常用来源：
| 经典 | 查找方式 |
|------|---------|
| 《周易·说卦传》 | web_search "说卦传 第X章 原文" |
| 《周易·系辞传》 | web_search "系辞传 原文 二与四同功" |
| 《尚书·洪范》 | web_search "洪范 五行 原文" |
| 《黄帝内经·素问》 | web_search "素问 阴阳应象大论 五行" |
| 邵雍《梅花易数》 | web_search "梅花易数 体用总诀 原文" |
| 朱熹《周易本义》 | web_search "周易本义 卦序 八宫" |

### 2.2 交叉比对
搜索至少 2 个不同来源的现代解读：
- 学术论文/古籍注释（优先）
- 权威易学网站
- 避免：自媒体碎片化解读

### 2.3 记录
- 确认无误的知识点 → 编入教学材料
- 发现的谬误 → 记录到 `pitfalls`
- 存疑的 → 放弃该题，不强行出

---

## 第三步：开发关卡

### 3.1 编写教学材料
在 `index.html` 的 `LEVELS` 数组中添加新关卡数据。格式：
```javascript
{
  id: 3, icon: '👨‍👩‍👧‍👦', title: '八卦人物类象',
  desc: '乾父坤母震长男…',
  unit: 1,
  source: '《周易·说卦传》第十章',
  verified: true,
  pitfalls: ['网上说兑为中女是错的——兑为少女'],
  reviewCount: 2,
  questions: [ /* 20题 */ ],
  teachingContent: { /* 教学材料 */ }
}
```

### 3.2 出题原则
- 每题 4 个选项
- 正确选项必须有原文依据
- 干扰项须合理（不能太离谱）
- 每卦/每知识点至少覆盖 2 题
- 题目类型混合（不要太单一）

### 3.3 记忆曲线复习题
从 `state.completedLevels` 按间隔权重随机抽旧题。

---

## 第四步：本地测试

```bash
cd /home/ubuntu/meihua-pwa
python3 -m http.server 8899 &
# 在浏览器打开 http://127.0.0.1:8899
```

测试清单：
- [ ] 目录页可看到新关卡
- [ ] 教学页内容正确
- [ ] 开始答题后可正常作答
- [ ] 正确/错误反馈正常
- [ ] 完成页显示正确率
- [ ] 返回目录状态更新
- [ ] 温故知新题出现

---

## 第五步：部署

### 5.1 推送到 GitHub
```bash
cd /home/ubuntu/meihua-pwa
GIT_SSH_COMMAND="ssh -i /home/ubuntu/.ssh/meihua_gh -o StrictHostKeyChecking=no" \
  bash -c 'git add -A && git commit -m "第X关: 标题" && git push origin main'
```

### 5.2 同步到 Gitee
```python
import subprocess, base64, json, urllib.parse
token = "c221a49e85ec705f63c41c7dd50437ea"
api = "https://gitee.com/api/v5/repos/zweizweizwei/meihua-xuetang/contents/index.html"
# 1. GET sha
# 2. PUT 更新（access_token + content(base64) + sha + message）
```

### 5.3 验证
- 打开 https://zweizweizwei.github.io/meihua-xuetang/ 确认可用

---

## 第六步：更新大纲

在 `SYLLABUS.md` 中：
- 标记当前关为 ✅
- 更新「全局状态追踪」
- 为下一关写出开工清单

---

## 快速参考

| 项目 | 值 |
|------|-----|
| 工作目录 | `/home/ubuntu/meihua-pwa/` |
| 大纲文件 | `SYLLABUS.md`（本文件旁边） |
| 主代码 | `index.html` |
| GitHub SSH | `/home/ubuntu/.ssh/meihua_gh` |
| Gitee token | `c221a49e85ec705f63c41c7dd50437ea` |
| 当前进度 | 第50关完成 → 第51关待开发 |
