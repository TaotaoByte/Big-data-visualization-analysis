# 天气大数据管理系统
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Django](https://img.shields.io/badge/Django-4.2%2B-green)
![License](https://img.shields.io/badge/License-MIT-yellow)


## 项目新地址
项目移植到了https://github.com/TaotaoByte/weather_bigdata_admin

## 项目介绍
本项目是基于 Python Django 框架开发的**天气大数据管理系统**，聚焦解决气象数据管理效率低、可视化程度不足、海量数据查询分析繁琐等行业痛点，实现气象数据的全生命周期管理（录入、存储、查询、分析、可视化），为气象数据运维与分析决策提供一站式支撑。

系统定位为轻量化、易扩展的天气数据管理后台，适配中小规模气象数据管理场景，支持多维度气象指标（气温、降水、风力、湿度等）的管理与可视化，降低非技术人员的数据分析门槛。

## 技术栈
| 模块       | 技术/工具                                                                 |
|------------|--------------------------------------------------------------------------|
| 后端       | Python 3.8+、Django 4.2+、MySQL 8.0+（数据存储）、SQLAlchemy（可选）|
| 前端       | HTML5、CSS3、JavaScript、jQuery、ECharts 5.x（数据可视化）、Django Templates |
| 开发/部署  | Git、Pip、Virtualenv、Nginx（可选，生产环境部署）|

## 环境要求
- 操作系统：Windows/Linux/macOS
- Python 版本：3.8 及以上
- 数据库：MySQL 8.0+（或 SQLite 用于本地测试）
- 依赖管理：pip 20.0+

## 安装与部署
### 1. 克隆代码仓库
```bash
git clone https://github.com/your-username/weather-data-management-system.git
cd weather-data-management-system
```

### 2. 创建并激活虚拟环境
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/macOS
python3 -m venv venv
source venv/bin/activate
```

### 3. 安装项目依赖
```bash
pip install -r requirements.txt
```
> 若未提供 `requirements.txt`，可手动安装核心依赖：
> ```bash
> pip install django==4.2.7 mysqlclient==2.2.0 pillow==10.1.0 echarts-python==0.1.0
> ```

### 4. 配置数据库
1. 打开项目根目录下的 `settings.py`，修改数据库配置：
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'weather_db',  # 你的数据库名
        'USER': 'root',        # 你的数据库用户名
        'PASSWORD': 'your-password',  # 你的数据库密码
        'HOST': '127.0.0.1',   # 数据库地址
        'PORT': '3306',        # 数据库端口
    }
}
```
2. 在 MySQL 中创建数据库：
```sql
CREATE DATABASE weather_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 5. 数据迁移与初始化
```bash
# 生成迁移文件
python manage.py makemigrations

# 执行数据库迁移
python manage.py migrate

# （可选）创建超级管理员（用于后台管理）
python manage.py createsuperuser
```

### 6. 运行项目
```bash
python manage.py runserver 0.0.0.0:8000
```
运行成功后，访问 `http://127.0.0.1:8000` 即可进入系统首页，访问 `http://127.0.0.1:8000/admin` 进入 Django 后台管理页面（需超级管理员账号）。

## 核心功能
| 功能模块       | 详细说明                                                                 |
|----------------|--------------------------------------------------------------------------|
| 数据管理       | 支持气象数据的增删改查、批量导入/导出（Excel/CSV），适配观测/统计类多维度数据 |
| 数据查询分析   | 支持多条件组合查询（时间、地区、气象指标），优化大数据量下的查询性能       |
| 可视化看板     | 基于 ECharts 实现气温、降水、风力等指标的折线图/柱状图/地图可视化展示     |
| 系统管理       | 用户权限控制、数据备份/恢复、系统日志查看                                 |
| 性能优化       | 数据库索引优化、SQL 查询逻辑优化，解决海量数据检索卡顿问题                 |

## 项目目录结构
```
weather-data-management-system/
├── manage.py               # Django 项目核心管理文件（启动/迁移/创建应用等）
├── weather_system/         # 项目主配置目录
│   ├── __init__.py
│   ├── settings.py         # 项目配置（数据库、静态资源、应用注册等）
│   ├── urls.py             # 全局 URL 路由配置
│   ├── asgi.py             # ASGI 部署配置
│   └── wsgi.py             # WSGI 部署配置
├── data_manage/            # 数据管理应用（核心业务模块）
│   ├── models.py           # 气象数据模型定义
│   ├── views.py            # 视图函数（业务逻辑处理）
│   ├── urls.py             # 应用内 URL 路由
│   ├── forms.py            # 数据表单验证
│   └── migrations/         # 数据库迁移文件
├── templates/              # 前端模板文件（HTML）
│   ├── index.html          # 系统首页/可视化看板
│   ├── data_query.html     # 数据查询页面
│   └── admin_panel.html    # 后台管理面板
├── static/                 # 静态资源目录
│   ├── css/                # 样式文件
│   ├── js/                 # 交互脚本（含 ECharts 可视化）
│   └── images/             # 静态图片
├── requirements.txt        # 项目依赖清单
└── README.md               # 项目说明文档
```

## 使用说明
### 1. 数据导入
- 进入「数据管理」模块，点击「批量导入」按钮，上传符合模板格式的 Excel/CSV 文件（模板可在系统内下载）。
- 系统自动校验数据格式，校验通过后完成导入，可在「数据列表」查看导入结果。

### 2. 数据查询
- 进入「数据查询」模块，选择查询条件（如时间范围、地区、气象指标类型），点击「查询」按钮获取结果。
- 支持查询结果的导出、可视化展示切换。

### 3. 可视化看板
- 系统首页默认展示可视化看板，支持切换不同气象指标（气温/降水/风力等）、时间维度（日/周/月）查看数据趋势。
- 看板支持数据下钻，点击图表可查看明细数据。

## 待优化/扩展方向
- [ ] 接入第三方气象 API，实现自动拉取实时气象数据
- [ ] 增加数据预测功能（基于机器学习模型）
- [ ] 支持多租户权限管理
- [ ] 前端升级为 Vue/React 框架，提升交互体验
- [ ] 完善生产环境部署文档（Docker 容器化部署）

## 许可证
本项目采用 MIT 许可证开源 - 详见 [LICENSE](LICENSE) 文件。

## 致谢
- Django 官方文档：https://docs.djangoproject.com/
- ECharts 官方文档：https://echarts.apache.org/
- 气象数据公开数据源（如中国天气网）

## 联系方式
若有问题或建议，可通过以下方式联系：
- GitHub Issues：https://github.com/TaotaoByte/Big-data-visualization-analysis/issues
- 邮箱：2042184732@qq.com
```

### 使用说明
1. 替换文档中的 `your-username`、`your-password`、`your-email@example.com` 为你自己的 GitHub 用户名、数据库密码、邮箱；
2. 若项目中使用了其他可视化库/数据库（如 SQLite 而非 MySQL），需对应修改技术栈、数据库配置部分；
3. 若有 `requirements.txt` 文件，建议补充实际依赖包（可通过 `pip freeze > requirements.txt` 生成）；
4. 可根据实际需求补充截图（如系统可视化看板、数据管理页面），增强 README 可读性（截图可上传到项目仓库，用相对路径/URL 引用）。
