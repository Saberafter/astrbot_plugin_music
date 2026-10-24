# 本 fork 维护说明

上游是 `Zhalslar/astrbot_plugin_music`，原作者和 MIT 许可证保持不变。

## 改了什么

- QQ/OneBot 的本地语音直接发送 `file://` 文件 URI。
- QQ/OneBot 的语音链接直接交给 OneBot 接收端下载并发送。
- 两个分支都绕过 AstrBot 通用 `Record` 接口的 WAV/base64 转换。
- 其他平台继续使用原流程，原有发送顺序和失败回退不变。

这不代表完全不转码，NapCat 仍可能按 QQ 的要求处理音频。
本地语音依赖 AstrBot 和 NapCat 能读取同一个绝对路径。
不同服务器或不同挂载路径不满足这个条件，可以优先使用语音链接。

## 分支

- `main`：跟踪上游，不能直接在这里加定制修改。
- `codex/onebot-direct-audio`：维护补丁，也是本 fork 的默认分支。
- 当前基线：上游 `8a9a92da0b6fe7040edf4bb5f67aabfd7385c7a1`，版本 `v3.1.0`。
- fork 版本：`v3.1.0+directaudio.1`。

截至 2026-10-24，上游已经有 3.2.0。本次没有顺带升级，后续需合并评估。

## 安装与升级

通过仓库地址 `https://github.com/Saberafter/astrbot_plugin_music` 安装。
AstrBot 的安装来源也要设为这个仓库，不能只修改 `metadata.yaml`。
后台升级和批量升级都应继续从本 fork 下载，不要切回官方市场源。

升级前先提醒维护者合并上游，保留定制修改：

```sh
git fetch upstream
git switch main
git merge --ff-only upstream/main
git push origin main
git switch codex/onebot-direct-audio
git merge main
```

处理冲突后，确认两个 OneBot 语音分支仍在，`metadata.yaml` 的仓库仍指向本 fork。
上游版本变化时，沿用新的版本号并保留 `+directaudio.N` 后缀。
然后推送定制分支，再去 AstrBot 后台升级并热重载点歌插件。

不要强制同步或重置定制分支，也不要把 `main` 设为部署默认分支。
不自动合并，不自动升级线上，不把“插件加载成功”当作“歌曲已经发送成功”。
