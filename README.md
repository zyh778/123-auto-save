# <div align="center"><img src="img/icon.png" width="120" alt="夸克自动转存助手"></div>

## <div align="center">夸克自动转存助手</div>

<div align="center">

一个功能强大的夸克网盘自动转存工具，支持定时追更、智能重命名、插件扩展等功能。

[![Python](https://img.shields.io/badge/Python-3.6+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/Cp0204/quark_auto_save.svg)](https://github.com/Cp0204/quark_auto_save)

</div>

## ✨ 主要特性

### 🔁 自动转存与追更
- **智能监控**：自动监控夸克分享链接，及时转存新内容
- **增量更新**：仅转存新增文件，避免重复操作
- **批量管理**：支持多任务并行处理

### 🎯 智能过滤与重命名
- **正则匹配**：强大的正则表达式匹配功能
- **魔法重命名**：支持多种变量替换（集数、季数、日期等）
- **智能排序**：自动文件排序，确保命名一致性
- **扩展名处理**：可配置忽略扩展名进行重复检测

### 🌐 Web 管理界面
- **可视化配置**：直观的 Web 界面管理任务
- **实时监控**：查看转存进度和执行日志
- **定时任务**：基于 APScheduler 的定时任务调度
- **远程管理**：支持远程访问和控制

### 🔌 插件系统
- **扩展架构**：支持自定义插件扩展功能
- **丰富插件**：内置 Emby、Plex、AList 等多种插件
- **热插拔**：支持插件动态加载和配置
- **优先级控制**：可配置插件执行优先级

### 📱 多平台支持
- **青龙面板**：完美适配青龙定时任务
- **Docker**：提供 Docker 镜像部署
- **本地运行**：支持 Windows、Linux、macOS
- **云服务器**：支持各种云服务器环境

## 🚀 快速开始

### 环境要求

- Python 3.6+
- pip 包管理器

### 安装步骤

1. **克隆项目**
```bash
git clone https://github.com/Cp0204/quark_auto_save.git
cd quark_auto_save
```

2. **安装依赖**
```bash
pip install -r requirements.txt
```

3. **配置文件**
```bash
# 首次运行会自动下载配置模板
python quark_auto_save.py
```

4. **编辑配置**
编辑 `quark_config.json` 文件，配置您的夸克 Cookie 和转存任务：

```json
{
  "cookie": "您的夸克Cookie",
  "push_config": {
    "CONSOLE": true
  },
  "tasklist": [
    {
      "taskname": "示例任务",
      "shareurl": "https://pan.quark.cn/s/xxxxxxxx",
      "savepath": "/自动转存",
      "pattern": ".*\\.(mp4|mkv|avi)",
      "replace": "{TASKNAME} - S{SXX}E{E}.{EXT}"
    }
  ]
}
```

### 青龙面板部署

1. **添加仓库**
```bash
ql repo https://github.com/Cp0204/quark_auto_save.git "quark_auto_save"
```

2. **设置定时任务**
```
0 8,18,20 * * * quark_auto_save.py
```

3. **配置环境变量**
- `QUARK_COOKIE`: 夸克 Cookie（仅签到）
- `QUARK_TEST`: 设置为 "true" 进行通知测试

### Docker 部署

```bash
docker run -d \
  --name quark-auto-save \
  -v $(pwd)/config:/app/config \
  -p 5000:5000 \
  cp0204/quark-auto-save:latest
```

## 📖 详细配置

### Cookie 获取

1. 登录 [夸克网盘](https://pan.quark.cn/)
2. 打开浏览器开发者工具 (F12)
3. 刷新页面，在 Network 标签找到请求
4. 复制请求头中的 `Cookie` 字段

### 任务配置参数

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `taskname` | string | ✅ | 任务名称 |
| `shareurl` | string | ✅ | 夸克分享链接 |
| `savepath` | string | ✅ | 保存路径 |
| `pattern` | string | ❌ | 正则匹配模式 |
| `replace` | string | ❌ | 重命名模板 |
| `startfid` | string | ❌ | 起始文件ID |
| `enddate` | string | ❌ | 任务结束日期 |
| `runweek` | array | ❌ | 运行星期 |
| `ignore_extension` | boolean | ❌ | 忽略扩展名检测 |

### 魔法变量说明

| 变量 | 说明 | 示例 |
|------|------|------|
| `{TASKNAME}` | 任务名称 | `我的剧集` |
| `{S}` | 季数（单数字） | `1` |
| `{SXX}` | 季数（双数字） | `S01` |
| `{E}` | 集数 | `05` |
| `{DATE}` | 日期 | `2024-01-01` |
| `{YEAR}` | 年份 | `2024` |
| `{EXT}` | 文件扩展名 | `mp4` |
| `{I+}` | 序号占位符 | `001, 002, 003` |

## 🔌 插件开发

### 插件接口

```python
class YourPlugin:
    def __init__(self, **config):
        self.default_config = {
            "enabled": True
        }
        self.config = {**self.default_config, **config}
        self.is_active = self.config.get("enabled", False)

    def run(self, task, account=None, tree=None):
        # 插件逻辑处理
        return task
```

### 内置插件

- **Emby**: 自动刷新 Emby 媒体库
- **Plex**: 自动更新 Plex 服务器
- **AList**: 同步文件到 AList
- **WebHook**: 发送 WebHook 通知

## 📊 Web 管理界面

访问 `http://localhost:5000` 进入 Web 管理界面：

- **任务管理**: 添加、编辑、删除转存任务
- **执行日志**: 查看详细的执行日志
- **系统状态**: 监控系统运行状态
- **配置管理**: 在线编辑配置文件

## 🔧 高级功能

### 定时任务配置

使用 APScheduler 支持多种定时方式：

```python
# 每天定时执行
scheduler.add_job(task_function, 'cron', hour=8, minute=0)

# 间隔执行
scheduler.add_job(task_function, 'interval', hours=2)

# 一次性执行
scheduler.add_job(task_function, 'date', run_date='2024-01-01 10:00:00')
```

### 通知配置

支持多种通知方式：

```json
{
  "push_config": {
    "CONSOLE": true,
    "SERVERCHAN": "您的 ServerChan Key",
    "BARK": "您的 Bark Token",
    "TG_BOT_TOKEN": "您的 Telegram Bot Token",
    "TG_USER_ID": "您的 Telegram User ID"
  }
}
```

## 🛠️ 故障排除

### 常见问题

1. **Cookie 失效**
   - 重新获取夸克 Cookie
   - 检查 Cookie 格式是否正确

2. **转存失败**
   - 检查分享链接是否有效
   - 确认保存路径是否有权限

3. **任务不执行**
   - 检查运行周期配置
   - 确认正则表达式是否正确

### 日志分析

程序运行日志包含详细信息：

```bash
# 查看完整日志
python quark_auto_save.py

# 查看特定任务
grep "任务名称" logs/quark_auto_save.log
```

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目基于 MIT 许可证开源 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🙏 致谢

- [Quark](https://pan.quark.cn/) - 夸克网盘服务
- [Flask](https://flask.palletsprojects.com/) - Web 框架
- [APScheduler](https://apscheduler.readthedocs.io/) - 任务调度
- [treelib](https://treelib.readthedocs.io/) - 树形数据结构

## 📞 联系方式

- 项目主页: [GitHub](https://github.com/Cp0204/quark_auto_save)
- 问题反馈: [Issues](https://github.com/Cp0204/quark_auto_save/issues)
- 讨论交流: [Discussions](https://github.com/Cp0204/quark_auto_save/discussions)

---

<div align="center">
  <p>如果这个项目对您有帮助，请给个 ⭐️ 支持一下！</p>
  <p>Made with ❤️ by Cp0204</p>
</div>