```markdown
# 加密二进制发布产物仓库

## 概述

`encrypted-binary-release-artifacts` 是一个用于集中存储和分发由私有源码仓库构建生成的**加密二进制发布产物（Encrypted Binary Release Artifacts）**的公共 GitHub 仓库。

本仓库作为多个软件项目统一的二进制发布渠道使用。

各项目的源码、开发资源以及 CI/CD 构建流程均维护在私有仓库中。本仓库仅发布经过：

- 自动化构建
- 加密打包
- 完整性校验
- 发布审核

后的最终二进制产物。

**本仓库不包含任何源代码。**

---

# 仓库用途

本仓库用于提供安全、标准化的软件二进制发布平台。

整体发布流程：

```

私有源码仓库
|
|
GitHub Actions
|
|
构建二进制产物
|
|
加密 & 打包产物
|
|
生成校验和 & 签名
|
|
发布 GitHub Release
|
|
加密二进制发布产物

```

---

# 仓库定位

本仓库支持多个独立软件项目共用。

每个项目拥有：

- 独立私有源码仓库
- 独立 CI/CD 构建流程
- 独立版本生命周期
- 独立 Release 管理

本仓库只负责存储最终发布产物。

---

# 仓库组织规范

多个项目通过 GitHub Release 进行管理。

示例：

```

encrypted-binary-release-artifacts

Release:

project-a-v1.0.0

```
Assets:

├── project-a-v1.0.0-linux-amd64.7z
├── project-a-v1.0.0-linux-arm64.7z
├── project-a-v1.0.0-windows-amd64.7z
└── SHA256SUMS
```

project-b-v2.1.0

```
Assets:

├── project-b-v2.1.0-linux-amd64.7z
└── SHA256SUMS
```

```

---

# Release 命名规范

所有 Release 必须遵循：

```

<ProjectName>-v<Version>

```

示例：

```

mytool-v1.0.0

server-agent-v2.3.0

backup-manager-v1.5.2

```

要求：

- 项目名称必须明确
- 版本号必须符合语义化版本规范
- 禁止使用无意义版本名称

---

# 二进制产物命名规范

所有发布文件统一采用：

```

<ProjectName>-<Version>-<OS>-<Architecture>.<Format>

```

示例：

```

mytool-v1.0.0-linux-amd64.7z

mytool-v1.0.0-linux-arm64.7z

mytool-v1.0.0-windows-amd64.7z

mytool-v1.0.0-darwin-arm64.7z

```

命名字段说明：

| 字段 | 说明 |
|-|-|
| ProjectName | 项目名称 |
| Version | 软件版本 |
| OS | 操作系统 |
| Architecture | CPU 架构 |
| Format | 压缩格式 |

---

# 支持平台

默认支持以下构建目标：

| 操作系统 | CPU 架构 |
|-|-|
| Linux | amd64 |
| Linux | arm64 |
| Windows | amd64 |
| macOS | arm64 |

根据项目需求，可以扩展其它平台。

例如：

- Windows ARM64
- macOS Intel
- FreeBSD
- RISC-V

---

# 产物安全规范

本仓库中的发布产物应遵循安全软件分发规范。

推荐采用：

- AES-256 加密压缩
- SHA256 完整性校验
- 数字签名
- 自动化 CI/CD 发布
- 构建来源追踪
- 可复现构建（条件允许）

示例：

```

mytool-v1.0.0-linux-amd64.7z

mytool-v1.0.0-linux-amd64.sha256

mytool-v1.0.0-linux-amd64.sig

```

---

# 加密策略

发布的二进制产物可以在上传前进行加密处理。

流程：

```

原始二进制文件

```
    |
    |
    v
```

加密压缩包

```
    |
    |
    v
```

GitHub Release Asset

````

加密后的发布包需要有效凭据才能解压。

没有正确的解密凭据：

- 无法读取文件内容
- 无法获取内部二进制文件
- 无法直接使用软件

---

# 完整性校验

用户下载发布文件后，应验证文件完整性。

## Linux / macOS

```bash
sha256sum -c SHA256SUMS
````

## Windows PowerShell

```powershell
Get-FileHash .\filename -Algorithm SHA256
```

验证目的：

* 防止文件传输损坏
* 防止文件被非法替换
* 确保下载文件完整可靠

---

# CI/CD 发布流程规范

所有接入本仓库的项目应遵循统一发布流程。

推荐流程：

```
私有源码仓库

        |
        v

代码检出

        |
        v

自动构建

        |
        v

自动测试

        |
        v

二进制打包

        |
        v

加密处理

        |
        v

生成校验文件

        |
        v

创建 Release

        |
        v

上传发布产物
```

---

# 版本管理规范

所有项目采用语义化版本：

```
MAJOR.MINOR.PATCH
```

示例：

```
v1.0.0

v1.2.5

v2.0.0
```

版本规则：

| 类型    | 说明          |
| ----- | ----------- |
| MAJOR | 不兼容的大版本变化   |
| MINOR | 新功能增加       |
| PATCH | Bug 修复和维护更新 |

---

# 源码管理策略

本仓库不存储任何源码。

源码统一维护于各项目私有仓库。

本仓库只包含：

* 编译后的二进制文件
* 加密发布压缩包
* SHA256 校验文件
* 数字签名文件
* Release 说明
* 构建元数据（如适用）

---

# 禁止发布内容

以下内容禁止上传：

* 源代码
* 私钥文件
* GitHub Token
* CI/CD 密钥
* 内部配置文件
* 环境变量文件
* 数据库凭据

敏感信息必须存储在：

* 私有仓库
* GitHub Secrets
* 密钥管理系统

中。

---

# 软件供应链安全

使用本仓库发布软件时，建议遵循现代软件供应链安全实践。

推荐：

* 私有源码仓库保护
* 自动化 CI/CD 构建
* Secret 安全管理
* 二进制签名
* 完整性验证
* 依赖漏洞扫描
* SBOM 软件物料清单生成

---

# 用户下载流程

标准用户流程：

```
1. 打开 GitHub Releases

2. 选择目标版本

3. 下载对应平台产物

4. 验证 SHA256

5. 解密并解压文件

6. 运行软件
```

---

# License

通过本仓库发布的每个项目拥有独立的软件许可证和使用协议。

所有二进制产物均遵循对应项目 License 约束。

---

# 维护说明

本仓库作为统一的软件二进制发布平台进行维护。

具体项目：

* 安装说明
* 使用文档
* 配置说明
* 技术支持

请参考对应项目文档。

---

# 维护者

由项目所有者维护。

本仓库提供安全、标准化的加密二进制软件发布渠道。
