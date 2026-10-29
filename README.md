# monthly-report

Claude Code 插件：根据 git 提交记录生成**月度绩效**。

- 按**你自己的模板**排版（大项、分值、a/b/c 小项、成果描述），不内置任何公司格式
- 读取你本人的提交，按功能主题归并、精简，给出分值建议；总分始终与模板一致
- 一个月有多个任务时，可拆分「当前项目」与「其他任务」的分值，其他任务由你口述后排版
- 对照上个月的历史，提示**重复**和**被取代**的功能点，避免绩效前后矛盾
- 也能先写**下月计划**，月底做总结时自动对照「计划 vs 实际」

## 安装

```
/plugin marketplace add lizhenmiao/monthly-report
/plugin install monthly-report@monthly-report
```

第一行添加插件市场（GitHub 仓库 [lizhenmiao/monthly-report](https://github.com/lizhenmiao/monthly-report)），第二行安装其中的 `monthly-report` 插件。安装后重启 Claude Code 或执行 `/reload-plugins` 生效。

## 使用

在任意 git 仓库里直接说：

```
/monthly-report 总结 2026-10
/monthly-report 规划 2026-11
```

或者自然语言：「帮我写 10 月的绩效」「写下个月的绩效计划」。

第一次使用会让你贴出自己的绩效模板并保存；之后每次会问「沿用上次模板，还是换了」。

## 数据存在哪里

模板和历史定稿保存在插件的持久数据目录（更新插件不会丢）：

```
<插件数据目录>/
├── template.md
└── history/
    └── <项目名>/
        ├── 2026-10.md        月度定稿
        └── 2026-11.plan.md   下月规划稿
```

- 插件数据目录是 Claude Code 提供的 `CLAUDE_PLUGIN_DATA`；取不到时回落到 `~/.claude/monthly-report/`
- 这些文件**只在你本机**，不会进入本仓库，也不会被上传
- 项目名取当前 git 仓库的目录名，同一个人在多个项目里使用互不干扰

## 说明

- 不需要任何脚本或运行时依赖，只用 `git`
- 它只读取 git 提交（以及你口述的内容）；其他仓库或非代码工作，需要你补充说明
- 分值只是**建议**，最终由你确认；定稿前不会保存任何文件

## 许可证

[MIT](LICENSE)
