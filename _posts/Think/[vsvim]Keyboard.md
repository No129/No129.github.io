# 先備知識
vsvim 

# 配置檔
## **查詢配置檔路徑**
```
:set vimrcPaths
```
一般應該是 **C:\\Users\[account]** 路徑。

## 新增配置檔
在檔案夾下新增一個文字檔，更改名稱為 *_vsvimrc* ( 是的，沒有副檔名 ) ，接著透過文字編輯器就可以將一般常用的設定放進去，重新啟動 Visual Studio 就會生效了。

```
"設定 <esc> 快捷鍵 jj ( 方便切換到 normal 模式 )
:inoremap jj <esc> 
```

