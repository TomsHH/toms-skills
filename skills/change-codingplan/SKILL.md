---
name: change-codingplan
description: |
  切换应用的配置套餐。当用户说"切换套餐"、"切换{app}套餐"、"换套餐"、"切换到xxx"等时触发。
  从 profiles.md 中读取预定义的套餐列表，让用户选择后将对应配置写入目标配置文件。

---

# change-codingplan - 通用配置套餐切换

## 用途

在预定义的多个配置套餐之间快速切换，修改目标应用的配置文件。

## 触发条件

用户请求切换套餐时使用，例如：
- "切换套餐"
- "切换 {app} 套餐"
- "换套餐"

## 工作流程

### 第一步：读取 profiles.md

从 skill 同目录下读取 `profiles.md`：
- `app` - 应用名称，用于提示信息
- `profile_name` - 套餐名称
- `target.path` + `target.file` - 目标配置文件完整路径
- `profiles` 数组 - 可用套餐列表（每个有 name、file、description）

### 第二步：让用户选择套餐

使用 `AskUserQuestion` 工具展示套餐选择列表：
- 选项数量 = `profiles` 数组长度
- 每个选项的 label 使用套餐的 `name` 字段
- description 使用套餐的 `description` 字段（如果有）

### 第三步：执行切换

1. 根据用户选择的套餐名称，找到对应的 `file`
2. 读取 skill 目录下 `settings/` 子目录中该 `file` 对应的配置文件
3. 解析 JSON 内容
4. 将内容写入到 `target.path` + `target.file` 拼接的目标路径（覆盖原文件）

### 第四步：确认完成

告知用户：
- 配置已成功写入
- **需要完全退出并重新启动 {app}** 才能生效
- 重启后可验证配置是否正确

## 文件结构

```
{skill-directory}/
├── SKILL.md              # 本文件，通用逻辑
├── profiles.md           # 应用和套餐定义
├── profiles.md.example   # 模板示例
└── settings/             # 套餐配置文件目录
    ├── profile-a.json
    └── profile-b.json
```

## 扩展到其他应用

为其他应用创建新的 skill 时：

1. 复制整个 skill 目录
2. 修改 `profiles.md`：
   - `app` 改为新应用名称
   - `target` 改为新应用配置路径
   - `profiles` 改为新应用的套餐列表
3. 在 `settings/` 目录中添加新应用的配置文件

## 示例

**用户说**：切换到 minimax-codingplan

**执行**：
1. 读取 profiles.md，发现 minimax-codingplan 对应 settings-minimax.json
2. 读取 settings/minimax.json 的内容
3. 写入到目标配置文件（如 C:\Users\<你的用户名>\.claude\settings.json）
4. 告知用户切换成功，需重启 vibe coding 工具
