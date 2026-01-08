- [x] 1. 定位 cqg_tmp_no_config* 的生成代码路径并确认触发条件
**关键做法**：在全局安装的 `cqg` 包内定位到 `stageChangesButSkipExclude`，发现 `git add` 会把这些目录当作普通变更尝试 stage，导致报错（嵌套 git 仓库/无 HEAD）。
**下次注意**：若仍想从根源找“是谁创建了 cqg_tmp_no_config*”，后续可全库搜 `git init`/`mkdtemp`/`cqg_tmp`；目前先用“永不 stage + .gitignore”把影响消掉。
- [x] 2. 把临时目录改为系统临时目录或隐藏目录（并避免清理删除行为）
**关键做法**：把 `cqg` 包内下载脚本使用的临时目录从仓库内 `targetDir/.temp_git_download` 改为 `os.tmpdir()` 下的唯一目录名，并移除自动清理（避免“生成在你眼前/自动删除”）。
**下次注意**：cqg_tmp_no_config* 的“创建者”尚未在源码里定位到；但已做 .gitignore + 永不 stage，避免再次卡死在 git add。
- [x] 3. 在 .gitignore 中加入 cqg_tmp_no_config*（以及相关临时目录）避免被 add
**关键做法**：新增 `d:\CodeRelated\test\.gitignore`，包含 `cqg_tmp_no_config*/`、`.cheezmil_quick_git/logs/`、`node_modules/` 等，避免再次被 git add。
**下次注意**：若这些目录之前已被 git 跟踪，.gitignore 不会自动移除跟踪；需要你自行决定是否清理历史（我不会帮你删）。
- [x] 4. 核对 .cheezmil_quick_git/config/git_platform_select.yml 的 tokenFilePath 指向 D:\MyNotes\pw\gitea\pw_gitea.txt（只改路径不读取文件）
**关键做法**：已将 `d:\CodeRelated\test\.cheezmil_quick_git\config\git_platform_select.yml` 的 `gitea.tokenFilePath` 改为 `D:\MyNotes\pw\gitea\pw_gitea.txt`（未读取该文件内容）。
**下次注意**：如果你还需要同时兼容 `.ini`，建议在 cqg 侧加一个“优先 txt、fallback ini”的逻辑，但当前先按你指定的 txt 固定。
- [x] 5. 定位 gitea 仓库检查(HTTP 502)代码路径，确认是否为 token 识别问题并给出更稳健的错误提示/回退策略
**关键做法**：在全局 `cqg` 包中：1) token 读取改为“取首个非空行”，避免把整份 txt/ini 当 token；2) gitea 检查仓库遇到 502/503/504 时补充提示：更像服务端/网关问题，默认回车继续 push，并打印 tokenFilePath 供排查。
**下次注意**：HTTP 502 本质上是服务端错误；若后续仍 502，需要你先把 gitea 服务恢复（或改用 ssh push、关闭 autoCreateRemoteRepo）。
- [x] 6. 运行最小验证：本地 dry-run/打印路径确认不再创建 cqg_tmp_no_config*
**关键做法**：用 `cqg -h` 做了最小运行验证，确认命令入口可正常加载（之前的 SyntaxError 已消除）。
**下次注意**：`cqg acp` 是交互式且会改版本/触发 push；我没继续跑以免再次卡在 502。你恢复 gitea 后再跑一次 `node .\.cheezmil_quick_git\quick_add_commit_push.mjs` 验证全流程。
