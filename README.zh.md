[English](./README.md) | 中文
### btc-wallet-stealer
- 助记词碰撞
- 不花钱，利用闲置机器
### 支持模式
| 币种  | 混合 | 在线 | 离线 |
|-----|:--:|:--:|:--:|
| BTC | x  | x  | ✓  |
| ETH | ✓  | ✓  | ✓  |
### 构建
- Git
- Golang 1.21
- 运行
  - `git clone https://github.com/ChengenH/btc-wallet-stealer.git`
  - `cd btc-wallet-stealer`
  - `git submodule update --init`
  - `go mod tidy`
  - `CGO_ENABLED=0 go build -ldflags "-s -w" .`
  - `chmod +x btc-wallet-stealer`
  - `./btc-wallet-stealer`
- 脚本
  - `sh build.sh`
### Docker镜像
- Linux AMD 编译
  - `CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags "-s -w" .`
- Linux ARM 编译
  - `CGO_ENABLED=0 GOOS=linux GOARCH=arm64 go build -ldflags "-s -w" .`
- 镜像构建
- `sudo docker build -f Dockerfile -t btc-wallet-stealer:v1.0 .`
### 程序运行
- 直接运行
    - `./btc-wallet-stealer`
- 容器运行
    - `sudo docker run -d  btc-wallet-stealer:v1.0`
### 配置文件说明
```markdown
{
  "mode":2, # 运行模式, 0:混合 1:在线 2:离线
  "wallet":{
    "eth":["wallet_path/xxx.txt"],
    "btc":["wallet_path/xxx.txt"]
  },
  "proxy": {  # 代理配置
    "enable": true, # 是否开启代理
    "address": "http://0.0.0.0:2334" # 代理地址
  },
  "words_list": "english", # 助记词语言
  "etherscan_api_key": "xxxxxxxx" # api key配置, 在线模式需要
}
```
### Description
- 运行这个程序不会有任何控制台输出，匹配到有余额的钱包地址，会将结果写入balance.txt文件中
### 感谢
- [hdkeygen](https://github.com/modood/hdkeygen)
### TODO
- 期待好的建议或者PR