# Before All
## 系统版本
Ventura 13.1 (22C65)

## 安装和升级 
```bash
brew install neovim
brew upgrade neovim --fetch=HEAD
```

## 常用查询功能（各操作系统通用）
在 vim 的命令模式，执行。  
- 配置保存位置 `:echo stdpath('config')`
```bash
~/.config/nvim
```
- 数据保存位置 `:echo stdpath('data')`
```bash
~/.local/share/nvim/site
```

## mac快捷键修改
1. 将 `CapsLock` 和 `Control` 换位（非必需）
2. 在 `iTerm2-->Settings-->Profiles-->Keys` 中将左右 `option` 键修改为 `meta` 键

# 配置总览 
  neovim 的配置文件位置在 `~/.config` 下面
  . config
  └─ nvim
     ├── init.lua // 初始化配置入口
     └── lua
	     ├── basic.lua // 基础配置
	     ├── keybindings.lua // 键盘映射
	     ├── lsp // 内置 LSP (Language Server Protocol)
	     │   ├── language_servers.lua
	     │   └── nvim-cmp-config.lua
	     ├── plugin-config // 插件配置
	     │   ├── bufferline.lua
	     │   └── nvim-tree.lua
	     └── plugins.lua // 插件管理配置

## init.lua
```lua
-- 基础设置
require('basic')
-- 快捷键映射
require('keybindings')
-- Packer插件管理(如果git访问不佳，可以用离线方式安装，此时不需要插件管理)
require('plugins')
-- 皮肤设置
require('zephyr')
-- 插件配置

-- LSP配置
```

## lua
### basic.lua
```lua
-- utf8
vim.g.encoding = 'UTF-8'
vim.o.fileencoding = 'utf-8'
-- jk移动时光标下上方保留8行
vim.o.scrolloff = 8
vim.o.sidescrolloff = 8
-- 使用相对行号
vim.wo.number = true
vim.wo.relativenumber = true
-- 高亮所在列和行
vim.wo.cursorcolumn = true
vim.wo.cursorline = true
-- 显示左侧图标指示列
vim.wo.signcolumn = 'yes'
-- 右侧参考线，超过表示代码太长了，考虑换行
vim.wo.colorcolumn = '80'
-- 缩进2个空格等于一个Tab
vim.o.tabstop = 2
vim.bo.tabstop = 2
vim.o.softtabstop = 2
vim.o.shiftround = true
-- >> << 时移动长度
vim.o.shiftwidth = 2
vim.bo.shiftwidth = 2
-- 新行对齐当前行，空格替代tab
vim.o.expandtab = true
vim.bo.expandtab = true
vim.o.autoindent = true
vim.bo.autoindent = true
vim.o.smartindent = true
-- 搜索大小写不敏感，除非包含大写
vim.o.ignorecase = true
vim.o.smartcase = true
-- 搜索不要高亮
vim.o.hlsearch = false
-- 边输入边搜索
vim.o.incsearch = true
-- 使用增强状态栏后不再需要 vim 的模式提示
vim.o.showmode = false
-- 命令行高为2，提供足够的显示空间
vim.o.cmdheight = 2
-- 当文件被外部程序修改时，自动加载
vim.o.autoread = true
vim.bo.autoread = true
-- 禁止折行
vim.o.wrap = false
vim.wo.wrap = false
-- 行结尾可以跳到下一行
vim.o.whichwrap = 'b,s,<,>,[,],h,l'
-- 允许隐藏被修改过的buffer
vim.o.hidden = true
-- 鼠标支持
vim.o.mouse = 'a'
-- 禁止创建备份文件
vim.o.backup = false
vim.o.writebackup = false
vim.o.swapfile = false
-- smaller updatetime 
vim.o.updatetime = 300
-- 等待mappings
vim.o.timeoutlen = 200
-- split window 从下边和右边出现
vim.o.splitbelow = true
vim.o.splitright = true
-- 自动补全不自动选中
vim.g.completeopt = 'menu,menuone,noselect,noinsert'
-- 样式
vim.o.background = 'dark'
vim.o.termguicolors = true
vim.opt.termguicolors = true
-- 不可见字符的显示，这里只把空格显示为一个点
vim.o.list = true
vim.o.listchars = 'space:·'
-- 补全增强
vim.o.wildmenu = true
-- Dont' pass messages to |ins-completin menu|
vim.o.shortmess = vim.o.shortmess .. 'c'
vim.o.pumheight = 10
-- always show tabline
vim.o.showtabline = 2
```

### keybindings.lua
```lua
-- 后面定义的快捷键 <Leader> 就表示空格
vim.g.mapleader = ' '
vim.g.maplocalleader = ' ' 
-- 保存本地变量
local map = vim.api.nvim_set_keymap
local opt = {noremap = true, silent = true}

-- 之后就可以这样映射按键了
-- map{'模式', '按键', '映射为xx', opt}

-- basic
map('n', '<C-u>', '10k', opt) -- ctl+u 向上移动10行
map('n', '<C-d>', '10j', opt) -- ctl+d 向下移动10行
map('i', 'jj', '<ESC>', opt) -- jj从insert退到normal
-- visual模式下连续缩进
map('v', '<', '<gv', opt) 
map('v', '>', '>gv', opt)
-- 分屏
map('n', 'sv', ':vsp<CR>', opt) -- 水平
map('n', 'sh', ':sp<CR>', opt) -- 垂直
-- 关闭分屏
map('n', 'sc', '<C-w>c', opt) -- 当前
map('n', 'so', '<C-w>o', opt) -- 其他
-- alt+hjkl 窗口跳转
map('n', '<A-h>', '<C-w>h', opt)
map('n', '<A-j>', '<C-w>j', opt)
map('n', '<A-k>', '<C-w>k', opt)
map('n', '<A-l>', '<C-w>l', opt)

-- plugins
-- 
```

### lsp
#### language_servers.lua
#### nvim-cmp-config.lua

### plugin-config
#### bufferline.lua
#### nvim-tree.lua

### plugins.lua
```lua
return require('packer').startup(function()
  -- Packer can manage itself
  use 'wbthomason/packer.nvim'
  use 'glepnir/zephyr-nvim'
end)
```

