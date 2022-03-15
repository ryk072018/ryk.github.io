# setup-ipsec-vpn + Vultr 实现科学上网

## 🍎使用Vultr

### 第一步：

> 注册 Vultr 账号

> 首页可选择中文。或者使用浏览器自带翻译

> 这个活动连接注册赠送$100


[![vultr](https://user-images.githubusercontent.com/27181965/158292988-2febcd03-2812-424b-a5ab-31c9dab1d29f.png)](https://www.vultr.com/?ref=9075619-8H)



### 第二步：

> 创建和部署服务器

![image-20220315073328274](https://user-images.githubusercontent.com/27181965/158284083-ad380c63-fe73-4b7a-8214-412d877659ff.png)

![image-20220315073403945](https://user-images.githubusercontent.com/27181965/158284091-8d97f82c-8466-4944-b853-e9b1ad12b4c8.png)

![image-20220315073426556](https://user-images.githubusercontent.com/27181965/158284093-ccfbc2d5-c30e-456d-9f98-e381a7dd953b.png)

---

---

## 🍊使用 setup-ipsec-vpn

###   [setup-ipsec-vpn github中文文档](https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/README-zh.md)

## 第一步：


1. 使用Xshell 连接到Vultr 参考下文ps2

- [Xshell Xftp 家庭/学校免费](https://www.xshell.com/zh/free-for-home-school/)


2. 在你的 Linux 服务器* （例子Ubuntu）

> 使用以下命令快速搭建 IPsec VPN 服务器：

> 你的 VPN 登录凭证将会被自动随机生成，并在安装完成后显示在屏幕上。	

```shell
wget https://git.io/vpnsetup -qO vpn.sh && sudo sh vpn.sh
```

## 第二步：

#### 使用辅助脚本配置 IKEv2

> 在Xshell输入

```shell
sudo ikev2.sh --auto
```

![xshell](https://user-images.githubusercontent.com/27181965/158284101-24d9ad94-ef7c-4b89-842d-a6257e3447cf.png)

## 第三步：

#### 配置 IKEv2 VPN 客户端

**Windows 8, 10 和 11** 用户可以自动导入 IKEv2 配置：

1. 将生成的 `.p12` 文件安全地传送到你的计算机。
2. 右键单击 [ikev2_config_import.cmd](https://github.com/hwdsl2/vpn-extras/releases/latest/download/ikev2_config_import.cmd) 并保存这个辅助脚本到与 `.p12` 文件 **相同的文件夹**。
3. 右键单击保存的脚本，选择 **属性**。单击对话框下方的 **解除锁定**，然后单击 **确定**。
4. 右键单击保存的脚本，选择 **以管理员身份运行** 并按提示操作。
5. 最后查看电脑自带VPN，连接自己配置的VPN开始Google 

> 遇到问题参考 [这里](https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/ikev2-howto-zh.md)



### ps1：.p12文件的传送： 使用XFTP 软件拖拽到本地文件夹

### ps2：Xshell 连接Vultr

> 新建-->主机-->连接

> 使用自己的主机IP 

![Vultr2 ](https://user-images.githubusercontent.com/27181965/158284096-1bbc94b2-c731-4c35-9a74-fa6c4999a24b.png)

![xshell 2](https://user-images.githubusercontent.com/27181965/158284099-c89c0d02-7e3d-4880-ade3-388c78b9706c.png)

