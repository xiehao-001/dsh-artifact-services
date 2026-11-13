# 成果服务（@eduwork/dsh-artifact-services）

> Studio 与其它插件共用的成果生成底座：Office、语音与视频渲染服务。
>
> Shared artifact backend for Office generation, speech and video rendering.

## 功能

提供文档/演示/表格生成与预览、TTS/ASR Provider 抽象、Remotion 视频渲染管线。单独安装可用于自建成果插件；Studio 会自动依赖它。

## 安装

```bash
# 在 DSH 中把本目录作为本地 bundle 安装（绝对路径）
```

安装后由 DSH 插件系统加载，条目 id 为 `dsh-artifact-services`。

## 依赖

- `@deepseek-ai/cordis`
- `@deepseek-ai/dsh-skill`
- `@deepseek-ai/dsh-tools`

## 兼容性

- `engines.dsh`: `>=0.2.1 <0.3.0`
- 与 EduWork 发行版同源，来源于 ECNU/EduWork 仓库。

## 许可

MulanPSL-2.0 AND MIT（与上游 EduWork 一致）。

## 入口修正


- 移除悬空声明：./video-template (./lib/video-template.js)
