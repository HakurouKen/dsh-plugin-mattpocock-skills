# dsh-plugin-mattpocock-skills

将 [mattpocock/skills][upstream] 转化为 dsh 插件。

[English](README.md) | **简体中文**

## 项目内容

一个 DeepSeek Harness 插件，把 [mattpocock/skills][upstream] 的全部技能加入你的会话目录。
不会往 `~/.agents/skills` 复制任何文件；上游标记 `disable-model-invocation` 的技能只能通过
`/名称` 调用，模型无法自行触达。

| | |
|---|---|
| 上游 | [github.com/mattpocock/skills][upstream]（MIT），每日同步 |
| DSH | `>=0.2.0-rc.1 <0.3.0-0` |
| 运行时依赖 | 无 |

## 谁需要它

**你已经用 Codex 插件装过 Matt Pocock 的技能，而不希望为了让 DSH 看到它们，再往
`~/.agents/skills` 里放第二份。**

Codex 把技能存在它自己的存储里，Harness 会话读不到。Harness 只从
`<project>/.dsh/skills`、`<project>/.agents/skills`、`~/.dsh/skills`、
`~/.agents/skills` 发现技能。把技能复制进其中一个是可行的，但会让同样的技能存在于两处、
各有更新路径，并逐渐不一致。本插件是另一种选择：DSH 无需第二份副本即可获得这些技能。

**不需要**的情况：如果技能已在 `~/.agents/skills` 或 `<project>/.agents/skills`，那些位置
优先级更高，本插件会被遮蔽，两份副本还会互相矛盾。请二者择一。

## 使用说明

```bash
dsh plugin --profile <profile> add dsh-plugin-mattpocock-skills
```

然后启用一次 bundle —— Web 界面 **插件 → Bundle**，或写入 `dsh.profile.bundles` ——
并重启 Harness。此后全部技能出现在会话目录中，可通过 `skill` 工具或 `/名称` 命令调用。

若要从本地检出安装，把包名换成它的路径即可：

```bash
dsh plugin --profile <profile> add /absolute/path/to/dsh-plugin-mattpocock-skills
dsh plugin --profile <profile> remove dsh-plugin-mattpocock-skills   # 卸载
```

---

插件代码为 MIT。技能为 MIT，版权归 Matt Pocock，上游许可证位于 `skills/LICENSE`；
详见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

本项目的维护工作 —— 同步上游、校验、发布 —— 均已自动化，见 `scripts/` 与
[`.github/workflows/release.yml`](.github/workflows/release.yml)。

[upstream]: https://github.com/mattpocock/skills
