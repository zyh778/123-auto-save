# 123自动转存

<div align="center">

![项目图标](img/icon.png)

**基于Flask + Vue.js的夸克网盘自动转存工具**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)](https://flask.palletsprojects.com)
[![Vue.js](https://img.shields.io/badge/Vue.js-2.x-brightgreen.svg)](https://vuejs.org)
[![License](https://img.shields.io/badge/License-AGPL-yellow.svg)](LICENSE)


</div>

## 📖 项目简介

**123自动转存** 是一个功能强大的夸克网盘自动转存工具，提供现代化的Web管理界面和智能的文件管理功能。支持正则表达式匹配、自动重命名、定时任务调度等高级特性，让你的网盘管理更加智能高效。

## ✨ 主要特性

### 🚀 核心功能
- **自动转存**: 智能识别夸克网盘分享链接并自动转存
- **正则匹配**: 强大的文件匹配和重命名规则引擎
- **任务管理**: 完整的任务CRUD操作和状态监控
- **定时调度**: 基于Cron表达式的灵活任务调度
- **实时日志**: Server-Sent Events实时任务执行日志

### 🌐 Web界面
- **现代化UI**: 基于Vue.js + Bootstrap 5的响应式设计
- **在线配置**: JSON配置文件在线编辑器
- **Cookie验证**: 实时测试Cookie有效性
- **任务建议**: 智能任务推荐和快速添加
- **文件管理**: 直观的文件浏览和管理界面

### 🔧 高级特性
- **魔法匹配**: 预定义的常用匹配模式
- **多账号支持**: 支持多个夸克账号管理
- **插件系统**: 可扩展的插件架构（当前版本已屏蔽）
- **媒体集成**: 支持媒体服务器识别和处理

## 🚀 快速开始

### 环境要求
- Python 3.8+
- 现代浏览器（Chrome、Firefox、Safari、Edge）

### 安装步骤

1. **克隆项目**
```bash
git clone https://github.com/your-repo/123-auto-save.git
cd 123-auto-save
```

2. **安装依赖**
```bash
pip install -r requirements.txt
```

3. **配置Cookie**
- 打开浏览器访问 `pan.quark.cn`
- 按F12打开开发者工具
- 复制完整的Cookie字符串
- 编辑 `config/quark_config.json` 文件，填入你的Cookie

4. **启动服务**
```bash
python app/run.py
```

5. **访问管理界面**
打开浏览器访问：`http://localhost:5005`

## 📋 使用指南

### Cookie配置格式
```json
{
  "cookie": [
    "你的完整Cookie字符串"
  ]
}
```

### 任务配置示例
```json
{
  "taskname": "我的转存任务",
  "shareurl": "https://pan.quark.cn/s/xxxxx",
  "savepath": "/我的文件/转存目录",
  "pattern": "$TV_REGEX",
  "replace": "",
  "enddate": "2099-12-31"
}
```

### 定时规则
```bash
# 每天8点、18点、20点执行
"crontab": "0 8,18,20 * * *"

# 每周一至周五的9点执行
"crontab": "0 9 * * 1-5"

# 每2小时执行一次
"crontab": "0 */2 * * *"
```

## 🛠️ 功能模块

### Web管理界面
- **登录认证**: 安全的用户登录和会话管理
- **配置管理**: 在线JSON配置编辑器
- **任务管理**: 任务列表的增删改查
- **实时监控**: 任务执行状态的实时更新
- **手动执行**: 即时触发指定任务执行

### 核心转存引擎
- **Quark API**: 完整的夸克网盘API封装
- **智能匹配**: 支持正则表达式的文件匹配
- **自动重命名**: 基于规则的智能文件重命名
- **批量处理**: 高效的批量文件转存
- **错误处理**: 完善的异常处理和重试机制

### Cookie验证系统
- **实时测试**: 点击按钮即时验证Cookie有效性
- **用户信息**: 显示Cookie对应的用户昵称
- **状态反馈**: 直观的测试结果提示
- **错误诊断**: 帮助快速定位Cookie问题

## 📁 项目结构

```
123-auto-save/
├── app/                    # Web服务模块
│   ├── run.py            # Flask应用入口
│   ├── templates/        # HTML模板
│   │   ├── index.html   # 主页面
│   │   └── login.html   # 登录页面
│   └── static/           # 静态资源
│       ├── css/         # 样式文件
│       ├── js/          # JavaScript文件
│       └── img/         # 图片资源
├── config/               # 配置文件目录
│   └── quark_config.json # 主配置文件
├── img/                  # 项目图片
│   ├── icon.png         # 项目图标
│   └── screenshot.png   # 截图
├── quark_auto_save.py   # 核心转存逻辑
├── quark_config.json     # 配置模板
├── requirements.txt       # Python依赖
└── README.md            # 项目说明
```

## 🎯 使用场景

### 📚 资料收集
- 自动收集学习资料和文档
- 批量下载课程视频和电子书
- 智能分类和整理学习资源

### 🎬 媒体管理
- 影视剧集的自动分类存储
- 按规则重命名媒体文件
- 定时获取新发布的剧集

### 💾 数据备份
- 重要资料的自动备份
- 多渠道数据同步
- 定时备份任务调度

## 🔧 配置说明

### 基础配置
```json
{
  "cookie": [
    "b-user-id=xxx; _UP_A4A_11_=xxx; __uid=xxx;"
  ],
  "crontab": "0 8,18,20 * * *",
  "webui": {
    "username": "admin",
    "password": "admin123"
  }
}
```

### 高级配置
```json
{
  "magic_regex": {
    "$TV_REGEX": {
      "pattern": ".*?([Ss]\\d{1,2})?(?:[第EePpXx\\.\\-\\_\\( ]{1,2}|^)(\\d{1,3})(?!\\d).*?\\.(mp4|mkv)",
      "replace": "\\1E\\2.\\3"
    }
  },
  "tasklist": [
    {
      "taskname": "自动转存",
      "shareurl": "分享链接",
      "savepath": "/目标目录",
      "pattern": "",
      "replace": "",
      "enddate": "2099-12-31"
    }
  ]
}
```

### 环境变量
| 变量名 | 说明 | 默认值 |
|--------|------|--------|
| `HOST` | 服务监听地址 | `0.0.0.0` |
| `PORT` | 服务端口 | `5005` |
| `DEBUG` | 调试模式开关 | `false` |
| `CONFIG_PATH` | 配置文件路径 | `./config/quark_config.json` |

## 🐛 故障排除

### 常见问题

**Q: Cookie如何获取？**
A:
1. 打开浏览器访问 `pan.quark.cn`
2. 登录你的夸克账号
3. 按F12打开开发者工具
4. 切换到Network标签页
5. 刷新页面，找到任意请求
6. 复制Request Headers中的Cookie字符串

**Q: 任务执行失败怎么办？**
A:
1. 检查Cookie是否有效（使用测试按钮）
2. 确认分享链接是否有效且未过期
3. 检查目标路径是否存在权限
4. 查看实时日志了解具体错误信息

**Q: 定时任务不执行？**
A:
1. 检查Cron表达式格式是否正确
2. 确认服务程序持续运行
3. 查看系统时间和任务时间配置
4. 检查任务是否已被禁用

**Q: Web界面无法访问？**
A:
1. 检查服务是否正常启动
2. 确认端口是否被占用
3. 检查防火墙设置
4. 尝试使用 `http://localhost:5005` 访问

## 🤝 贡献指南

欢迎提交Issue和Pull Request！

### 开发流程
1. Fork 项目
2. 创建功能分支
3. 提交更改
4. 创建Pull Request

### 代码规范
- 遵循PEP 8代码风格
- 添加适当的注释和文档
- 确保代码通过测试
- 保持提交信息清晰

## 📄 开源协议

本项目采用 [AGPL License](LICENSE) 开源协议。
