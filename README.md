# 项目管理看板

一个简单的项目管理和进度跟踪工具。

## 主要功能

- 项目卡片展示，支持按分类和负责人查看
- 添加和编辑项目信息、进度记录
- 高优先级任务标记（每人只能设置一个）
- 筛选功能：待开发项目、高优先级项目
- 响应式设计，支持移动端使用

## 技术实现

- 前端：HTML/CSS/JavaScript（无框架）
- 后端：Supabase（数据库 + 认证）
- 单页面应用，约2700行代码

### 核心数据结构
```javascript
// 项目数据
{
  id: 1,
  name: "项目名称",
  description: "项目描述", 
  category: "分类名",
  status: "dev" | "done",
  owner: ["负责人1", "负责人2"],
  source: "github链接",
  milestones: [
    { date: "2024-01-01", text: "完成xxx" }
  ],
  high_priority_owners: ["设置为高优先级的负责人"]
}
```

## 本地运行

```bash
git clone https://github.com/molchip-tpr/molchip_ai_roadmap.git
cd molchip_ai_roadmap
python3 -m http.server 8000
```

访问 http://localhost:8000

## 数据库配置

需要在Supabase中创建`projects`表：

```sql
CREATE TABLE projects (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  description TEXT,
  category TEXT,
  status TEXT DEFAULT 'dev',
  owner JSONB DEFAULT '[]',
  source TEXT,
  milestones JSONB DEFAULT '[]',
  high_priority_owners JSONB DEFAULT '[]',
  last_updated TIMESTAMP DEFAULT NOW()
);
```

## 开发相关

这个项目使用Claude-4-Sonnet辅助开发完成。主要的开发思路：

1. 从基础的卡片展示开始
2. 逐步添加编辑、筛选功能
3. 实现高优先级任务的唯一性约束
4. 优化移动端体验

如果你想开发类似的工具，建议：
- 先实现核心的数据展示和编辑
- 再添加筛选、排序等辅助功能
- 最后处理响应式和交互优化

代码结构比较简单，所有逻辑都在一个HTML文件中，便于理解和修改。 