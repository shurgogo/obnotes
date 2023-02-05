1. 下载.msi 文件安装；或者.zip 文件解压后将 nvim.exe 所在 bin 加为环境变量，比如我是 `D:\Neovim\bin`，就将这个路径加到系统变量的 Path 下
 ![[NvimAddToPath.png]]
2. 使用 `powershell` 作为 terminal，注意不是 `windows powershell`
3. 打开 nvim，执行 `:checkhealth` ，有 WARNING，要手动到该路径下添加 `init.vim`
![[NvimConfWarn.png]]
4. vim-plug 插件安装
> 参考 https://github.com/junegunn/vim-plug
```powershell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni "$(@($env:XDG_DATA_HOME, $env:LOCALAPPDATA)[$null -eq $env:XDG_DATA_HOME])/nvim-data/site/autoload/plug.vim" -Force
```
5. 配置 `init.vim`