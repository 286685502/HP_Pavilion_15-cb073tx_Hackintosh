# HP_Pavilion_15-cb073tx_Hackintosh

这是我使用的惠普光影精灵3黑苹果引导文件，包含了Clover和OpenCore双引导。

## 电脑配置

CPU: Intel Core i5-7300HQ

GPU: Intel HD Graphics 630（Nvidia GeForce GTX 1050 已屏蔽）

声卡: ALC295（layout-id = 23）

网卡: Broadcom 94360CS2 + Realtek RTL8111

## Clover配置说明

Clover版本为5104，驱动目前最新。

这个EFI中CLOVER/kexts/other只保留了必要的驱动，Intel蓝牙驱动在CLOVER/kexts/off里面，有需要的话建议安装完成后再添加到other中。

啰嗦模式默认开启，安装完成后可以将启动参数-v删除。

重新把电池补丁放在了SSDT-BATT.aml中，亮度快捷键放在了SSDT-FN.aml中，避免因为DSDT冲突导致打过补丁的DSDT无法使用。

睡眠补丁在SSDT-GPRW.aml中，默认不启用。如果BIOS版本为F.18应该可以正常睡眠，旧版BIOS存在睡眠秒醒问题。有需要请自行修改config.plist以启用。

USB端口已经打过补丁，不影响USB3.0速率。

添加了风扇转速显示补丁SSDT-FANS.aml，但只能显示转速，无法通过软件控制。

序列号已经洗白，但已经被使用过。请参照教程自行洗白。机型建议不用修改。

注意，SmUUID和CustomUUID已经暂时留空，填写说明见下！

## OpenCore配置说明

OpenCore版本为0.5.6，驱动目前最新。

在使用这个EFI前请确保你对于CLOVER和OC引导有了足够的了解，能够应对一些突发状况并会自救。

所有的ACPI补丁全部拆出来放在了SSDT里面，大多数和clover差不多，而且更严谨。少数补丁由于OC中ACPI改名问题不通用。

由于OC默认所有操作系统使用同一套DSDT，所以有时会出现无法引导Windows的现象。通过SSDT-OC-XOSI.aml补丁对DSDT中操作系统参数设置为Win 10即可正常引导。（相关说明可在宪武大佬的项目 https://github.com/daliansky/OC-little 中看到）

睡眠补丁在SSDT-GPRW.aml里，默认不启用。BIOS低于F.18版本可能存在睡眠秒醒问题，请自行启用。

序列号和Clover里的是同一份，记得自己洗白。

注意，SystemUUID已经暂时留空，填写说明见下！

## Clover中SmUUID/CustomUUID和OC中SystemUUID填写说明

详见远景论坛帖子 http://bbs.pcbeta.com/viewthread-1838605-5-1.html 的 85 楼。

该操作主要为了避免使用OC引导Windows时因为主板UUID注入变化导致激活信息失效的问题。

按照maojinbing大佬的说法，Clover中的CustomUUID和OC中的SystemUUID应该填写主板的UUID，在Windows系统PowerShell中执行 wmic csproduct get uuid 即可获得。

Clover中的SmUUID（硬件UUID）可以暂时不填写。正常情况下，MLB和ROM一致的话，SmUUID的值不会改变。所以在洗白并且填写正确的CustomUUID（Clover）/ SystemUUID（OC）之后，可以在 关于本机-系统报告-硬件概览 中看到此时的硬件UUID，复制并填入config中的SmUUID即可。

## ALC295_PlugFix

用于修复耳麦二合一插孔插入耳麦时无法切换到外置麦克风的问题，内有使用说明。

## 交流群

惠普电脑装Mac交流群:543758684

OpenCore技术交流群:538643249
