# Wikifactory-Alias

> 本仓库为独立的非官方 Wikifactory 相关资料/社区项目，与 wikifactory.com 及其运营方无任何关联，不代表官方立场，亦不用于任何商业目的。本站/本项目不提供任何产品开发、CAD 协作或制造对接服务。

[Wikifactory](https://wikifactory.top) 的**页面别名**映射仓库（公开）。

别名让用户手输的「非正式路径」也能落到正确页面，并作为**搜索次要命中**出现在结果里。
映射由维护者**手动维护**；本仓库不含任何站点代码，构建时由站点同步读取。
别名的目标来自公开的内容仓库 [Wikifactory-Content](https://github.com/hellokug2699/Wikifactory-Content)。

## 格式

- 按游戏分文件，文件名即 `<游戏>.yml`，放在**仓库根目录**（例：`Satisfactory.yml`）
- 文件内容为**扁平映射**，每行一条 `别名路径: 目标键`
- **键与值都是「以站点根为基准的完整路径」**，不带首尾斜杠

```yaml
# Satisfactory.yml
Satisfactory/Buildings/foo: Satisfactory/Buildings/MAM   # 跨目录（可加简称前缀）
foo: Satisfactory/Buildings/MAM                          # 根级前缀
MAM: Satisfactory/Buildings/MAM                          # 目标 = 内容页面 id
satisfactory: Satisfactory                               # 目标 = 游戏 id
satis-buildings: Satisfactory/Buildings                  # 目标 = 分类键 <游戏>/<分类>
```

| 项 | 说明 |
| --- | --- |
| 键（别名路径） | 用户手输 URL 时命中的路径；跨目录 / 跨游戏不限，例 `Satisfactory/Buildings/foo` 或 `foo` |
| 值（目标键） | 内容页面 id（`<游戏>/<分类>/<...>/<页面>`）、游戏 id（`<游戏>`），或分类键（`<游戏>/<分类>`） |

文件可写 `#` 整行注释；值可用单 / 双引号包裹，或带 ` #` 行尾注释（见上方示例）。

## 行为

| 手输路径 | 结果 |
| --- | --- |
| 真实页面 / 游戏 / 分类 | 进入对应页面 |
| 有效别名 | 重定向到目标内容 |
| 既非真实页面也非别名 | 落到 404 页 |

目标页会在标题下方列出其全部别名；搜索时命中词**仅**出现在别名中，会在结果名称下方标注「别名：」。

## 校验（仅警告）

冲突 / 无效别名（与真实路径冲突、彼此重名含大小写、目标不存在）**仅警告并在构建期丢弃**，
不阻断站点构建。本仓库不含校验脚本，警告详情由站点构建输出。

> ⚠️ 本仓库公开可读，**请勿提交任何密钥、令牌、凭据或个人隐私信息**。
