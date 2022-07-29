# windows-auto-
windows 开机自启程序注册脚本

```python
import win32api
import win32con
import sys
import pathlib

sys.setrecursionlimit(1000000)

BasePath = pathlib.Path(sys.argv[0]).parent

name = 'checker_ip'
path = str(BasePath / "checker.exe")  # 需要注册的开机自启程序 根据自己情况修改这儿即可
print(name, path)
KeyName = r'Software\\Microsoft\\Windows\\CurrentVersion\\Run'

try:
    key = win32api.RegOpenKey(win32con.HKEY_CURRENT_USER, KeyName, 0, win32con.KEY_ALL_ACCESS)
    win32api.RegSetValueEx(key, name, 0, win32con.REG_SZ, path)
    win32api.RegCloseKey(key)
except Exception as e:
    print(f'error！{e}')
print('success！')
input("回车退出")
```
