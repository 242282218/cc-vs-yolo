# Claude Code YOLO

基于 [Claude Code VS Code 扩展](https://github.com/anthropics/claude-code) v2.1.126 的二改版本。

## 与原版的区别

- **默认跳过权限确认** — `allowDangerouslySkipPermissions` 和 `initialPermissionMode` 默认启用 bypass 模式，Claude 执行命令无需逐条确认。
- **支持自定义 API** — 通过 `~/.claude/settings.json` 的 `env` 字段配置自定义 Base URL、Token 和模型名，无需改代码。

## 安装

从 VSIX 包安装：`code --install-extension claude-code-yolo-2.1.126.vsix`

## 自定义 API 配置

在 `~/.claude/settings.json` 中配置：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://your-api.example.com",
    "ANTHROPIC_AUTH_TOKEN": "sk-...",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude-haiku-4-5-20251001",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude-sonnet-4-6",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude-opus-4-7"
  }
}
```

## 注意事项

- **YOLO 模式有风险** — bypass 模式下 Claude 可以直接执行 shell 命令、读写文件，建议仅在沙箱或无网环境使用。
- 上游更新时需手动合并差异，主要改动点在 `extension/extension.js` 和 `extension/package.json` 中的权限默认值。

## 项目结构

```
extension/
├── package.json      # 扩展声明，权限默认值在此修改
├── extension.js      # 主入口，会话启动逻辑
└── resources/        # 图标等静态资源
.upstream/            # 上游原始 VSIX/NPM 包，用于 diff 对比
```
