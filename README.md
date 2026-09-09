# **📁 AI 原理知识库 \- 项目改名与维护指南**

本文档包含了项目文件改名说明、添加新视频的数据结构说明以及本地运行注意事项。

## **1\. 🏷️ 项目改名说明**

如果需要重命名项目中的核心文件或修改网页标题，请参阅以下位置：

### **修改 JSON 数据文件名**

默认加载的数据文件名为 vids.json。若将其重命名（例如改为 videos\_data.json），需要同步修改 index.html 中的 Fetch 请求路径：

在 index.html 中找到：

const res \= await fetch('./vids.json');

修改为：

const res \= await fetch('./videos\_data.json'); // 替换为您重命名后的 JSON 文件路径

### **修改网页标题与 Branding**

在 index.html 中可以修改全局展示名称：

1. \<title\>AI 原理与算力视频合集 \- AI MindHub\</title\>  
2. \<h1 class="font-bold text-base text-white leading-none"\>AI 原理知识库\</h1\>

## **2\. 📝 向 vids.json 添加新视频格式**

每次添加新视频时，只需在 vids.json 的数组中追加以下结构的 JSON 对象：

{  
  "id": 4,  
  "title": "【视频标题】",  
  "bvid": "BVxxxxxxxx",  
  "aid": "123456789",  
  "cid": "987654321",  
  "originalUrl": "https://www.bilibili.com/video/BVxxxxxxxx/",  
  "category": "分类名称 (如：大模型与Transformer)",  
  "difficulty": "入门 / 进阶 / 深入 / 哲学",  
  "summary": "视频核心内容摘要与简介...",  
  "knowledgePoints": \[  
    { "time": "00:00", "text": "核心知识点 1 描述" },  
    { "time": "03:15", "text": "核心知识点 2 描述" }  
  \],  
  "tags": \["标签1", "标签2", "标签3"\],  
  "dateAdded": "2026-03-09"  
}

### **如何获取 B 站视频的 aid 与 cid？**

1. 在 B 站视频页面点击 **“分享” \-\> “嵌入代码”**，复制代码。  
2. 提取里面的 aid 和 cid 参数即可填入 vids.json。  
3. 或者直接把 B 站视频链接或嵌入代码发给 AI，由 AI 自动生成上述 JSON 并更新！

## **3\. 🌐 本地预览与 CORS 说明**

由于现代浏览器的安全策略，使用 file:// 协议直接双击打开本地 index.html 时，异步 fetch('./vids.json') 可能会受到跨域限制。

### **推荐的本地预览方式：**

1. **VS Code Live Server**：在 VS Code 中右键 index.html 点击 **"Open with Live Server"**。  
2. **Python 本地服务器**：在项目目录下运行终端命令：  
   python \-m http.server 8000

   然后在浏览器打开 http://localhost:8000 即可。

> **提示**：如果直接双击 index.html 打开，页面已内置 Fail-Safe 兜底机制，也会正常加载备用数据展示。
