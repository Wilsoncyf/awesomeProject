# awesomeProject

一个使用 Go 语言编写的简单示例项目，展示了环境搭建、模块管理和基础语法。

## 特性

- 🐹 基于 Go Module（`go.mod`）的项目结构
- 👋 简单的 “Hello, Go” 命令行程序
- 🔢 演示 `for` 循环与算术运算
- 🐳 支持 Docker 多阶段构建，部署为轻量镜像
- 🧪 包含基础测试示例（后续可扩展）

## 目录结构

```

awesomeProject/
├── .idea/               # GoLand IDE 配置（无需提交到版本库可 .gitignore）
├── go.mod               # Go Module 描述文件
├── go.sum               # 依赖校验和文件（自动生成）
├── main.go              # 程序入口示例
└── helloworld           # 编译生成的可执行文件（可加入 .gitignore）

````

## 快速开始

1. 克隆仓库
   ```bash
   git clone https://github.com/Wilsoncyf/awesomeProject.git
   cd awesomeProject
   ```

2. 安装依赖（模块会自动下载）

   ```bash
   go mod tidy
   ```

3. 运行示例

   ```bash
   go run main.go
   ```

4. 编译为可执行文件

   ```bash
   go build -o helloworld main.go
   ./helloworld
   ```

## Docker 化部署

```dockerfile
# 构建阶段
FROM golang:1.23-alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o server main.go

# 运行阶段
FROM scratch
COPY --from=builder /app/server /server
EXPOSE 8080
ENTRYPOINT ["/server"]
```

构建并运行镜像：

```bash
docker build -t awesomeproject .
docker run --rm -p 8080:8080 awesomeproject
```

## 贡献

欢迎 Issues 和 Pull Requests！

* 请先 Fork 本仓库
* 提交 PR 前，请确保通过 `go fmt`、`go vet`、`go test`

## 作者

* Chen Yongfeng (Wilson)
* GitHub: [Wilsoncyf](https://github.com/Wilsoncyf)
