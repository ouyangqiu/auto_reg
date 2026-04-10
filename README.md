# Any Auto Register

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12+-blue.svg?style=for-the-badge" alt="Python" />
  <img src="https://img.shields.io/badge/Node.js-18+-green.svg?style=for-the-badge" alt="Node.js" />
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="License" />
</p>

<p align="center">
  <a href="README.md">🇬🇧 English Version</a>
</p>

---

## 🙏 致谢

本项目是在以下优秀开源项目基础上的三开版本，在此衷心感谢原作者们的贡献：

- **一开项目**：[lxf746/any-auto-register](https://github.com/lxf746/any-auto-register) by @lxf746
- **二开项目**：[zc-zhangchen/any-auto-register](https://github.com/zc-zhangchen/any-auto-register) by @zc-zhangchen
- **临时邮箱方案**：[dreamhunter2333/cloudflare_temp_email](https://github.com/dreamhunter2333/cloudflare_temp_email)

本项目在前作基础上进行了功能扩展和优化。

---



## 🚀 快速开始

### 环境要求

- **Python**: 3.12 或更高版本
- **Node.js**: 18 或更高版本
- **Conda**: 推荐用于环境管理
- **Git**: 用于克隆仓库

### 方法一：一键部署（推荐）

```bash
# 1. 克隆项目
git clone https://github.com/dsclca12/auto_reg.git
cd auto_reg

# 2. 执行部署脚本
./deploy.sh
```

部署完成后访问 http://localhost:8000

### 方法二：手动安装

#### 1. 克隆项目
```bash
git clone https://github.com/dsclca12/auto_reg.git
cd auto_reg
```

#### 2. 创建 Python 环境
```bash
# 使用 Conda（推荐）
conda create -n any-auto-register python=3.12 -y
conda activate any-auto-register

# 或使用 venv
python3 -m venv any-auto-register-env
source any-auto-register-env/bin/activate  # Linux/Mac
```

#### 3. 安装依赖
```bash
pip install -r requirements.txt
```

#### 4. 安装浏览器
```bash
python -m playwright install chromium
python -m camoufox fetch
```

#### 5. 安装前端依赖
```bash
cd frontend
npm install
npm run build
cd ..
```

#### 6. 配置环境变量
```bash
cp .env.example .env
# 编辑 .env 文件，填入你的配置
```

#### 7. 启动服务
```bash
python main.py
```

访问 http://localhost:8000

---

## ⚙️ 配置说明

### 环境变量

复制 `.env.example` 到 `.env` 并按需配置：

```bash
# 服务器配置
HOST=0.0.0.0
PORT=8000
APP_RELOAD=0
APP_CONDA_ENV=any-auto-register

# 验证码服务
YESCAPTCHA_CLIENT_KEY=your_client_key
LOCAL_SOLVER_URL=http://127.0.0.1:8889

# 代理（可选）
PROXY_URL=http://username:password@ip:port

# 邮箱服务（根据需要配置）
MOEMAIL_API_KEY=your_api_key
SKYMAIL_API_KEY=your_api_key
SKYMAIL_DOMAIN=your_domain
```

### 邮箱服务

| 服务 | 标识 | 说明 | 需要配置 |
|------|------|------|---------|
| **LuckMail** | `luckmail` | 基于 API 的临时邮箱服务 | 是 |
| **MoeMail** | `moemail` | 默认选项，自动临时邮箱 | 是 |
| **TempMail.lol** | `tempmail_lol` | 临时邮箱，部分地区可能需要代理 | 否 |
| **SkyMail (CloudMail)** | `skymail` | 通过 API/Token/域名使用 | 是 |
| **YYDS Mail / MaliAPI** | `maliapi` | 支持域名和自动域名策略 | 是 |
| **GPTMail** | `gptmail` | 通过 GPTMail API 生成临时邮箱 | 是 |
| **DuckMail** | `duckmail` | 临时邮箱服务 | 是 |
| **Freemail** | `freemail` | 自建邮箱服务 | 是 |
| **Laoudo** | `laoudo` | 固定邮箱服务 | 是 |
| **CF Worker** | `cfworker` | 自建 Cloudflare Worker 邮箱 | 是 |

#### 📧 Kiro 邮箱要求

Kiro 风控严格，邮箱方案显著影响成功率：

- **自建邮箱**：100% 成功率 ✅
- **内置临时邮箱**：0% 成功率 ❌

**建议**：Kiro 使用自建邮箱（CF Worker、SkyMail）。

### 验证码服务

| 服务 | 说明 | 配置 |
|------|------|------|
| **YesCaptcha** | 第三方验证码解决服务 | 需要 Client Key |
| **本地 Solver** | 内置 Turnstile 解决器（camoufox + quart） | 随后端自动启动 |

### 外部系统集成

| 系统 | 说明 | 配置 |
|------|------|------|
| **CPA** | Codex Protocol API 管理面板 | API URL + Key |
| **Sub2API** | API 中转管理 | API URL + Key |
| **Team Manager** | 团队管理 | - |
| **grok2api** | Grok token 管理 | API URL + Key |

---



## 📡 API 文档

启动服务后访问 http://localhost:8000/docs 查看交互式 API 文档（Swagger UI）。

### 主要端点

| 端点 | 方法 | 说明 |
|------|------|------|
| `/api/accounts` | GET/POST | 账号管理 |
| `/api/tasks` | GET/POST | 任务管理 |
| `/api/platforms` | GET | 列出支持的平台 |
| `/api/proxies` | GET/POST | 代理管理 |
| `/api/config` | GET/PUT | 配置管理 |
| `/api/actions` | POST | 执行操作 |
| `/api/integrations` | GET/POST | 外部集成 |
| `/api/solver/status` | GET | Solver 状态 |
| `/api/solver/restart` | POST | 重启 Solver |

---

## 🔧 常见问题

### Turnstile Solver 未运行

**症状**：验证码验证失败，Solver 状态显示离线

**解决方案**：
1. 检查后端是否正确启动
2. 确保在正确的 Python 环境中运行（推荐 Conda 环境）
3. 验证 camoufox 已安装：`python -m camoufox fetch`
4. 查看 `backend.log` 中的 Solver 日志

### 端口被占用

**症状**：服务启动失败，端口 8000 已被占用

**解决方案**：
```bash
# 停止现有服务
pkill -f "python main.py"

# 或查找并终止特定进程
lsof -i :8000
kill <PID>

# 重启服务
python main.py
```

### 邮箱服务失败

**症状**：无法接收验证码

**解决方案**：
1. 检查代理配置和网络连接
2. 部分服务需要代理访问
3. 验证 API Key 是否正确
4. 尝试其他邮箱服务

### 被拒绝（ChatGPT）

**错误**：`registration_disallowed` 或 HTTP 400

**解决方案**：
1. 🔄 **更换代理 IP**（当前 IP 可能被标记，建议使用住宅代理）
2. 📧 **更换邮箱服务商**（临时邮箱域名可能已被拉黑）
3. ⏱️ **降低频率**（增加 30-60 秒随机延迟）
4. 🔃 **清除浏览器数据**或更换设备指纹
5. 📋 **减少批量大小**（建议每批最多 5 个）

### 数量限制

- 最大值：每批 1000 个账号
- 建议：使用随机延迟（10-30 秒）
- 最佳实践：每批 5-10 个账号，延迟 30-60 秒

### TLS/SSL 错误

**症状**：期间连接错误

**解决方案**：
1. 检查代理是否可用
2. 更新依赖：`pip install -r requirements.txt --upgrade`
3. 重新安装浏览器：`python -m playwright install chromium`

---

## 🛠️ 开发指南

### 添加新平台

1. 在 `platforms/` 目录创建新平台插件
2. 实现 `BasePlatform` 接口
3. 使用 `@register` 装饰器

示例：
```python
from core.registry import register, BasePlatform

@register
class MyPlatform(BasePlatform):
    name = "my_platform"
    display_name = "My Platform"
    
    async def register(self, config):
        # 实现代码
        pass
```

### 前端开发

```bash
cd frontend

# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 访问 http://localhost:5173

# 生产环境构建
npm run build
```

### 后端开发

```bash
# 激活 Conda 环境
conda activate any-auto-register

# 启动自动重载
export APP_RELOAD=1
python main.py
```

### 运行测试

```bash
pytest tests/
```

---

## 🐳 Docker 部署

### 环境要求

- Docker 20.10+
- Docker Compose 2.0+

### 快速开始

```bash
# 构建并启动
docker-compose up -d

# 查看日志
docker-compose logs -f

# 停止服务
docker-compose down
```

### 环境变量

```bash
# 在 docker-compose.yml 或 .env 中配置
SOLVER_BROWSER_TYPE=camoufox
CLIPROXYAPI_PORT_BIND=8317
GROK2API_PORT_BIND=8011
```

### 卷挂载

| 主机路径 | 容器路径 | 说明 |
|---------|---------|------|
| `./data` | `/runtime` | 运行时数据 |
| `./_ext_targets` | `/_ext_targets` | 外部目标 |
| `./external_logs` | `/app/services/external_logs` | 外部日志 |

---


<p align="center">
  <strong>⚠️ 再次提醒：请合法合规使用本项目，作者不对任何滥用行为负责</strong>
</p>
