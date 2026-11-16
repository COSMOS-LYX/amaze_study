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

##分支练习（feature/word-count）
从 main 拉出功能分支：git checkout -b feature/word-count
在分支上改代码（如 word-count.py）、改 README，然后：
git add .
git commit -m "new word count"
第一次推送该分支时要指定远程并设置上游：
git push -u origin feature/word-count
之后在同一分支再推，直接 git push 即可。
注意：git push -u 后面第一个参数是远程名（通常是 origin），不是分支名。
错误示例：git push -u feature/word-count  （Git 会把 feature/word-count 当成远程仓库）
正确示例：git push -u origin feature/word-count
推送成功后可在 GitHub 上从该分支创建 Pull Request 合并回 main。

##网络连接 bug 检查（Git 连不上 GitHub）
现象1：HTTPS 推送失败
fatal: unable to access 'https://github.com/...': Recv failure: Connection was reset
或：Failed to connect to github.com port 443

排查步骤：
1. 看远程地址：git remote -v
2. 测网页能否打开：浏览器访问 https://github.com
3. 看本机是否开了代理（Clash / v2ray 等）。Windows 可在“Internet 选项 → 连接 → 局域网设置”看到代理，常见为 127.0.0.1:10808
4. 关键：Git 默认不走系统代理，需要单独配置：
git config --global http.proxy http://127.0.0.1:10808
git config --global https.proxy http://127.0.0.1:10808
5. 再测：git ls-remote origin HEAD
能列出 commit 就说明 HTTPS 通了，然后再 git push

代理关掉后若又不需要代理，取消配置：
git config --global --unset http.proxy
git config --global --unset https.proxy

现象2：改成 SSH 后报 Permission denied to deploy key
说明当前 SSH 公钥被加在某个仓库的 Deploy keys 上（只绑一个仓库），不能推其他仓库。
个人练习更省事的做法是继续用 HTTPS + 代理；若坚持用 SSH，把公钥加到账号的 SSH and GPG keys，而不是某个仓库的 Deploy key。
