# lcl_knowledge_database

个人自动化知识仓库
采用「每日记录 + AI自动归类」模式

## 项目结构

daily目录为知识积累入口，由lcl本人每日记录知识

其余目录为知识归类目录，如agent、数据库、服务治理等，每个目录下分为case和knowledge两个目录

### daily

每日知识记录入口。
文件命名格式：YYYYMMDD.md

**示例:**
2026年3月24日的记录 → 20260324.md

### 知识归类目录

有多个知识归类目录

AIAgent员工 会自动将 daily 中的记录进行分析、提取、归类：

- case/：存放真实工作案例
  一个案例一个md，完整记录现象、原因、处理过程、结论。

- knowledge/：存放知识点、原理、规范
  一个知识点一个md，必须标注来源（案例/日期），形成可追溯知识链路。


**示例:**
/数据库
/数据库/case
/数据库/case/仪表盘数据库冷备导致主从延迟.md
/数据库/knowledge
/数据库/knowledge/mysql主备架构.md

## 项目成员

1. lcl: 项目Owner: 负责记录daily知识积累，负责cr/mr AIAgent员工 的提交
2. 大黄: OpenClaw内网版: 1号员工，负责读取daily中的每日知识积累，进行分析、提取、归类，写入对应知识归类目录中，并提交合流到main，由lcl做cr/mr。