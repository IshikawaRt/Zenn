---
title: "相対パスからのインポートエラー"
---
## 問題
上位ディレクトリから他のディレクトリのモジュールをインポートする際、以下のコードでは正しくインポートできない。

```Text
C─User─Dir1
       ├─Root
       │ └─file1.py
       └─Dir2
          └─file2.py
      
```

```python
import os, sys

sys.path.append(os.path.join(*__file__.split("\\")[:-2]))
from Dir2 import file2
```

## 原因
os.path.join()のディレクトリ直下にバックスラッシュが入っていなかった。

```powershell
print(__file__.split("\\")[:-2])
['C:', 'User', 'Root','Dir1',  'file1.py']

print(os.path.join(*__file__.split("\\")[:-2]))
C:User\Root\Dir1\file1.py
```
## 対策
join関数を使用
```python
import os, sys

sys.path.append("\\".join(*__file__.split("\\")[:-2]))
```
