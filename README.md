##环境创建
建立起python虚拟环境以及git环境
通过命令：python -m venv .venv创建了.venv文件夹
然后通过里面的脚本：venv\Scripts\Activate.ps1激活虚拟环境
创建git：git init，这样在工作区下建立了.git的隐藏文件
通过gitignore做好准备，首先创建.gitignore 里面写：.venv/ 和 __pycache__/  表示之后使用git add .不上传这些文件
建立github仓库，之后远程联系起来：git remote add origin https://github.com/COSMOS-LYX/amaze_study
通过命令：git remote -v  查看远程连接的远程仓库
使用通过add挑出需要存放的东西，放入暂存区
通过commit正式向git提交，存成一个版本，通过-m告诉版本信息“feat：新功能；docs：文档；fix：bug修复；refactor：重构；chore：杂项”
通过push提交到远程仓库
版本管理：修改本地分支为main：git branch -M main;提交到远程主分支：git push -u origin main