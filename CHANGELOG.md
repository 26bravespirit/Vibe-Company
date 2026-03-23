# Changelog

All notable changes to the Vibe Iteration Coach skill will be documented in this file.

## [4.0.0.0] - 2026-03-23

### Added
- **Mode 0: 新手引导** — 自动激活的初学者教练模式，使用 Core 5 技巧（T03, T06, T11, T14, T15）以直觉可理解的中文名称引导新用户
- **成长阶段系统** — 新手 → 入门 → 熟练 → 专家，基于会话次数、技巧使用数和评分的自动毕业标准
- **Coaching Hook** — 每个 Mode 执行后自动检测 4 种行为模式（全盘接受、缺少验证、重复打转、格式先行）并给出即时教练提示
- **简化评估模式** — 新手/入门阶段使用 3 维交通灯评估（表达清晰度、改进意识、做出选择）替代完整 6 维 10 分制
- **Expert Override** — 5 种触发词绕过 Mode 0 直接进入完整模式
- **初学者症状 S18-S20** — "我不知道怎么开始"、"AI写的不像我"、"不确定什么时候算完了"
- **初学者场景映射** — 首次创作、日常文档、会议纪要 3 个新场景
- **beginner-guide.md** — 5 个核心技巧的完整初学者友好说明
- **companion-mode.md** — Coaching Hook 的完整检测规则和分阶段提示语规范
- **persistence-layer 扩展** — 新增 skill_level、coaching_hooks_triggered、graduated 字段
- **v4/ 文件夹** — 完整的 v4 版本独立目录，原始 src/ 文件未修改

### Changed
- evaluation-framework.md 增加简化版评估模式（向后兼容）
- scene-mapping.md 增加 3 个初学者场景行
- technique-finder.md 增加 S18-S20 初学者症状
- persistence-layer.md 增加 3 个新字段（向后兼容，旧日志缺失字段默认 null）
