
Claude Code 自定义 Skills 集合，用于扩展和增强 Claude Code CLI 的能力。

### 一，已有 Skills

#### 1， change-codingplan — 通用配置套餐切换

在多个预定义的 API 配置套餐之间快速切换，一键修改 Claude Code 的配置文件（`settings.json`）。

**支持的套餐：**

| 套餐名称 | 说明 |
|---|---|
| MiniMax-CodingPlan | 使用 MiniMax 提供的模型服务 |
| 质谱-CodingPlan | 使用质谱提供的模型服务 |
| Ali-CodingPlan | 使用阿里提供的模型服务 |

**使用方式：** 在 Claude Code 中说"切换套餐"、"换套餐"或"切换到 xxx"即可触发。

##### 1.1， 如何扩展配置套餐

1. 复制 `skills/change-codingplan/` 目录
2. 修改 `profiles.md` 中的 `app`、`target` 和 `profiles` 字段
3. 在 `settings/` 目录下添加对应的 JSON 配置文件

### 二，项目结构

```
toms-skills/
├── README.md
└── skills/
    └── change-codingplan/       # 配置套餐切换 skill
        ├── SKILL.md             # Skill 逻辑定义
        ├── profiles.md          # 套餐与应用配置
        ├── profiles.md.example  # 配置模板示例
        └── settings/            # 各套餐的配置文件
            ├── ali.json
            ├── minimax.json
            └── zai.json
```

### 三，如何添加新的 Skill

1. 在 `skills/` 目录下创建新文件夹
2. 编写 `SKILL.md` 定义触发条件和工作流程


