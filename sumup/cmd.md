# cmd命令记录

## 端口进程关闭
`for /f "tokens=5" %%a in ('netstat -aon ^| find ":2091" ^| find "LISTENING"') do taskkill /f /pid %%a`

## 休息，等待几秒

`timeout 2`

TIMEOUT /t 2

## 最小化cmd窗口，启动

`start /min a.exe`

`start "" /min /wait "a.exe" -param1`

## 进入bat脚本目录
cd /d %~dp0

## 查找进程，强杀进程
tasklist |findstr "lash"
taskkill /FI "IMAGENAME eq core-service*" /F

## 调用其他bat脚本
call g.bat

## 批处理判断并自动获取管理权限

核心思想就是试图访问需要管理员身份才可以访问的资源，可以访问则有权限，不可以访问则没有权限

```
:: 方式一 powershell
REG QUERY "HKU\S-1-5-19">NUL 2>&1||(powershell -Command "Start-Process '%~sdpnx0' -Verb RunAs"&&exit)

:: 方式二 VBS
REG QUERY "HKU\S-1-5-19">NUL 2>&1||mshta vbscript:CreateObject("Shell.Application").ShellExecute("cmd.exe","/c %~s0 ::","","runas",1)(window.close)&&exit
```

## 创建桌面快捷方式

使用vbs

`mshta VBScript:Execute("Set a=CreateObject(""WScript.Shell""):Set b=a.CreateShortcut(a.SpecialFolders(""Desktop"") & ""\abcd.lnk""):b.TargetPath=""%~sdp0abcdPDFEditor.exe"":b.WorkingDirectory=""%~sdp0"":b.Save:close")`

## 注册表，操作
```
reg add "HKLM\Software\abcd Software\abcd PDF Editor" /f /v "BundleLang" /d "chs" >NUL 2>NUL
reg add "HKLM\Software\abcd Software\abcd PDF Editor" /f /v "BundleLang" /d "chs" /reg:32 >NUL 2>NUL
reg add "HKLM\Software\abcd Software\abcd PDF Editor" /f /v "InstallPath"  /d "%~dp0\" /reg:32 >NUL 2>NUL
reg delete "HKCU\Software\abcd Software" /F>NUL 2>NUL
```

## 强制删除文件夹
rd/s/q "%Temp%\abcd PDF Editor"2>NUL

## 注册dll，com组件
regsvr32 /s "%~dp0plugins\manExt_64.dll"

## 片段记录，后面在整理

```
@ECHO OFF&(PUSHD "%~DP0")&(REG QUERY "HKU\S-1-5-19">NUL 2>&1)||(
powershell -Command "Start-Process '%~sdpnx0' -Verb RunAs"&&EXIT)
```

```
net stop abcdPDFUpdateService >NUL 2>NUL
sc delete abcdPDFUpdateService >NUL 2>NUL 
```

taskkill /f /im PDFEditor* >NUL 2>NUL