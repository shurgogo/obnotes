美化
1. 安装 `nerd` 字体
	仓库：[[https://github.com/ryanoasis/nerd-fonts]]
	
2. 安装 `winget`
	1.  在线安装，应用商店搜“应用安装程序”

3. 安装 `oh-my-posh`
		`winget install oh-my-posh` 如果出现多个选项，执行
		`winget install --id  ${ID}

4. 修改 `PowerShell` 配置文件
使终端启动美化都能生效，以 `uew` 主题为例：
```bash
nvim $PROFILE

oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\uew.omp.json" | Invoke-Expression
```
其中 `$env:POSH_THEMES_PATH` 是安装后默认创建的环境变量，`--config` 的路径可以自定义，第二条命令可以在当前终端反复执行，方便查看效果

5. ENJOY!
 ![[ThemeUEW.png]]