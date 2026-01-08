- [x] 1. 确认scoop可用且bucket已就绪
**关键做法**：用一条命令同时检查scoop版本与bucket列表，快速确认环境就绪。
**下次注意**：若bucket列表不全再执行`scoop bucket add <name>`。
- [x] 2. 执行scoop安装ffmpeg-full
**关键做法**：先用`scoop search ffmpeg`确认是否存在`ffmpeg-full`清单；结果显示不存在时改装`ffmpeg`（下载的就是full_build包）。
**下次注意**：如果你坚持要装“nightly/gyan”版本，可改用`scoop install ffmpeg-nightly`或`scoop install ffmpeg-gyan-nightly`。
- [x] 3. 验证ffmpeg/ffprobe命令可用并输出版本
**关键做法**：用`ffmpeg -version; ffprobe -version; where.exe ffmpeg; where.exe ffprobe`一次性确认可执行文件与shim路径。
**下次注意**：若新开终端找不到命令，先跑`scoop reset ffmpeg`或检查环境变量PATH。
