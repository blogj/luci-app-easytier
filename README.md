# luci-app-easytier

依赖`kmod-tun``luci-lib-fs`需要先在系统软件包里安装好
### 快速开始
```bash
右上角Fork克隆本项目，去actions手动触发自动编译流程，2分钟后就能获取最新ipk压缩包`luci-app-easytier.zip`解压上传到Openwrt软路由安装即可
![actions界面](https://github.com/user-attachments/assets/7e5e843b-eb01-48f1-81ab-226a1418ca0f)


```
### 安装方法
```bash
#先上传到openwrt的/tmp/tmp目录里安装
opkg install /tmp/tmp/luci-app-easytier_all.ipk

#卸载
opkg remove luci-app-easytier

#更新版本需要先卸载再安装新的ipk然后去管理界面关闭插件 修改参数后重新点击应用并保存
#安装后openwrt管理界面里不显示easytier 请注销登录或关闭窗口重新打开  
```

此luci-app-easytier不包含二进制程序，需要自行在openwrt管理界面里的easytier插件界面里上传二进制程序

### 编译方法
```bash
#下载openwrt编译sdk到opt目录（不区分架构）
wget -qO /opt/sdk.tar.xz https://downloads.openwrt.org/releases/22.03.5/targets/rockchip/armv8/openwrt-sdk-22.03.5-rockchip-armv8_gcc-11.2.0_musl.Linux-x86_64.tar.xz
tar -xJf /opt/sdk.tar.xz -C /opt

cd /opt/openwrt-sdk*/package
#克隆luci-app-easytier到sdk的package目录里
git clone https://github.com/EasyTier/luci-app-easytier.git

cd /opt/openwrt-sdk*
#升级脚本创建模板
./scripts/feeds update -a
make defconfig

#开始编译
make package/luci-app-easytier/compile V=s -j1

#编译完成后在/opt/openwrt-sdk*/bin/packages/aarch64_generic/base目录里
cd /opt/openwrt-sdk*/bin/packages/aarch64_generic/base
#移动到/opt目录里
mv *.ipk /opt/luci-app-easytier_all.ipk
```
