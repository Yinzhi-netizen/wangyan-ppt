# Wangyan PPT for Codex

Wangyan 风格 PPT skill 的可安装分发版，包含六套设计预设、PPT Master 引擎、模板、图标与 hfsyapi 图片生成流程。

## 最简单的安装方式

把下面这段话发给你电脑上的 Codex：

> 请使用 $skill-installer，从 https://github.com/Yinzhi-netizen/wangyan-ppt 同时安装 skills/wangyan-ppt 和 skills/ppt-master，放在同一个用户级 skills 目录中，优先使用 ~/.agents/skills。不要只安装入口 skill。安装后阅读 wangyan-ppt/references/install.md，用同一个 Python 安装引擎 requirements.txt 的依赖，并完成不调用付费 API 的安装自检。不要覆盖已有同名 skill；如已有版本，请先报告并征得我的同意。图片服务密钥稍后由我在本机配置，不要从仓库寻找或输出密钥。

安装完成后新开一轮对话；若尚未识别 skill，重启 Codex。

如果仓库为私有，安装者需要先获得仓库访问权限，并在本机使用有权限的 GitHub 账号登录。不要把仓库访问令牌写进安装指令或分享给其他人。

## 使用

> 使用 $wangyan-ppt，根据这个提纲制作 PPT。保留原文，封面和章节页使用 AI 背景图。

明确的用户要求始终优先于预设。AI 图片会调用外部 hfsyapi 服务，需要单独的密钥和余额；Codex 登录本身不会为此流程提供图片服务密钥。未配置密钥时，不应静默更换供应商。

## 安装结构

```text
~/.agents/skills/
  wangyan-ppt/
  ppt-master/
```

两个目录必须相邻。PPT 项目输出保存在用户选择的工作目录，不要写进已安装的 skill 文件夹。

## 安全与来源

- 此仓库不包含历史 PPT 项目、私人文档、本机 .env、密钥或运行环境缓存。
- PPT Master 源自 [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)，MIT 授权；原作者版权与授权文本保留在根目录和两个 skill 内。
- 发布版保留当前引擎与 Wangyan 设计规则；仅补充跨电脑路径解析和安装说明。源机器上的原始工程不受影响。
- 这是本地 Codex skill 的 GitHub 分发包，不是已发布到插件商店的插件。

Codex skill 的官方发现与安装说明见 [Build skills](https://learn.chatgpt.com/docs/build-skills)。
