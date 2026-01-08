# 你每次务必遵守的规则

## 必须用简体中文回复我！必须用简体中文思考！

## 除了用户表明和AGENTS.md表明的特殊情况，其他情况禁止执行任何删除文件或文件夹的命令！！！禁止执行任何删除文件或文件夹的命令！！！禁止执行任何删除文件或文件夹的命令！！！必须让我手动确认删除，你不能帮我删除。所以，你务必在当前工作目录的“.cheezmil_task_manager\”文件夹中写一个“<时间精确到秒例如20251212_121212>.mjs”脚本,脚本示例：
```js
import path from 'node:path';
import { spawnSync } from 'node:child_process';
import { fileURLToPath } from 'node:url';
const selfPath = fileURLToPath(import.meta.url);
// 禁止访问这个index.js的内部逻辑。
const cliEntry = 'D:\\CodeRelated\\cheezmil-task-manager\\ctm-cli\\src\\index.js';
// 删除文件夹或文件的书写示例
const targets = [
  'D:\\CodeRelated\\test\\test-folder',
  'D:\\CodeRelated\\test\\test-file.md',
].map((p) => path.resolve(p));
const result = spawnSync(
  process.execPath,
  [cliEntry, 'recycle-to-trash-confirm', '--self-delete', selfPath, ...targets],
  { stdio: 'inherit' }
);
process.exit(result.status ?? 1);
```

## 如果代码文件是英文注释则修改或新增的文件都写英文注释，同理中文也是，除非用户有在本规则中其他地方有特殊说明。

## 禁止用chrome-mcp-tool搜索！上网搜索优先用mcphub exa这个工具，这个工具有时候会报错，没关系，必须再次尝试直到8次过后还是报错就放弃，若此时非常依赖搜索的内容才能进行写代码则必须停下来告诉用户这个工具失效了，若不依赖搜索的内容也能准确的修正代码则可以继续。我只是让你禁止用chrome-mcp-tool搜索，没让你不能打开具体的调试网页啊。

## 未经允许禁止写任何其他的md文档。

## 若项目所用编程语言支持跨平台，则你写的所有代码必须跨平台都能用。

## 若某些命令很难很多写成一行执行，或没法在一条命令中完成某些操作比如图片视频转换压缩，则必须在“D:\CodeRelated\tool_temp_code\<当前项目名称>\”这个文件夹中写一些临时的脚本文件，这种情况下，若使用到了python则务必使用环境变量的base环境，禁止创建新的虚拟环境。

## 若你在操作WSL，则禁止的操作有
- 未经允许禁止访问/mnt/任何windows挂载的盘符。

## 请你务必确认你写的代码生成的编译产物和各种依赖包比如node_modules这些文件夹注意一定要写到.gitignore中，避免这些不适合git add的文件夹或文件被add了。

## 有时候你会看到一些存储token或key的文件，禁止直接阅读这些文件，不准打印出来到控制台，不能直接把密钥内容硬编码到代码中，而是遵守用户的指示，一般是让程序自己直接从密钥的绝对路径读取。

## 禁止执行这些命令以及类似的命令：
git restore --source=HEAD --staged --worktree .






## 有一个CTM工具，这个CTM是给你用于列出超级详细的任务列表的，如果用户没有直接跟你表示“不要用CTM”，且除了用户表明的特殊情况之外，都默认必须用它，若无法CTM使用则告诉我。每完成一个任务，必须回来打勾，否则不能进行下一个任务！