# Clash-Verge-StaticIP-Guide
Clash Verge 静态住宅 IP 配置与测试教程

## 开始前需要准备的工具

- Clash Verge[最新下载地址](https://github.com/clash-verge-rev/clash-verge-rev/releases)
- 自己原来的机场订阅

## 开始配置

### 第一步：导入机场订阅

机场支持一键导入的话，直接导入即可。  
如果没有一键导入，就复制订阅文件链接，粘贴到 Clash Verge 中自行导入。

![1](https://github.com/user-attachments/assets/c8aab11e-5a92-4fbf-9d55-82ab9cc793c1)

### 第二步：提取机场文件代理组

打开 Clash Verge 左侧 **订阅** 页面，点击刚才导入的机场订阅文件，在弹出的快捷菜单中选择 **编辑文件**。

找到 `proxy-groups`，复制下面 **自动选择** 的整行内容（一般会有很多节点，内容较长），粘贴到新建的记事本文档中备用。

如果机场文件里没有 **自动选择** 这个名称，就找 `type` 类型为 `url-test` 的代理组并复制粘贴。

![2](https://github.com/user-attachments/assets/a74d6f6f-6f3d-4606-8cc5-e04ea48262c7)

![3](https://github.com/user-attachments/assets/49748b2d-28f3-407e-a482-09077998c9b6)

### 第三步：修改 Merge 文件

打开 Clash Verge 左侧 **订阅** 页面，进入 **全局扩展覆写配置**，将下面代码粘贴进去并替换原有代码。

说明如下：

- `商品卡77888` 是你自己创建的代理组名称，可以自行修改。
- `自动选择` 这一行，需要替换为你刚才复制到记事本中的内容。
- `payload` 下面定义的是你的静态住宅 IP。
- `Proxy-US` 是你的静态 IP 名称，可以自行修改。
- `server`、`port`、`username`、`password` 需要替换为你自己的实际信息。
- `server` 是 IP 地址。
- `port` 是端口。
- `username` 是用户名。
- `password` 是密码。

```yaml
profile:
  store-selected: true

proxy-groups:
  - { name: 商品卡77888, type: select, use: ["provider1"] }
  - { name: 自动选择, type: url-test, proxies: ['示例节点'], url: '', interval: 300 }

proxy-providers:
  provider1:
    type: inline
    override:
      dialer-proxy: 自动选择
    payload:
      - { name: Proxy-US, dialer-proxy: dialer, type: socks5, server: YOUR_SERVER, port: YOUR_PORT, username: YOUR_USERNAME, password: YOUR_PASSWORD }

rules:
  - MATCH,商品卡77888
```
<img width="865" height="671" alt="4" src="https://github.com/user-attachments/assets/c94c188c-82bc-4100-a1c9-af7aecffa1c6" />

### 第四步：测试节点

打开左侧 **代理** 页面，会显示你新创建的代理组以及静态住宅 IP 节点。点击选择后，使用 `check` 进行测速，查看节点延迟是否正常。

测试通过后，可以根据自己的需求选择 **规则模式** 或 **全局模式**。

最后打开左侧 **首页** 页面，在 **网络设置** 中开启 **系统代理**，代理就正式生效了。

![测试节点](https://github.com/user-attachments/assets/84eb1719-6ba9-46a3-abf4-9be798053ae9)

### 第五步：测试节点纯洁度

节点可以正常连通后，建议再通过以下网站检测 IP 纯洁度：（如图展示的是ping0的检测页面）

- [ping0](https://ping0.cc/)
- [ip2location](https://www.ip2location.com/demo)
- [ipinfo](https://ipinfo.io/)

<img width="1162" height="480" alt="b40714743bdd81ee26426e1899fc7605" src="https://github.com/user-attachments/assets/cd9d4a4b-1bb9-4727-b16e-01cffbf031af" />
