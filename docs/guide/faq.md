# 常见问题 {#title}

一些可能影响使用体验的问题和对应解决方案, 某些方案可能并不适用您的机型系统

如您有更好的方案或想对现有方案进行补充, 请点击底部 `为此页提供修改建议`

## 耗电说明 {#power}

首先 GKD 默认情况下并不耗电，有的人以为关闭更新检测，关闭日志就能减少耗电，并不正确

真正的耗电在于 启用的规则 和 当前应用界面无障碍节点数量及无障碍事件刷新频率

如果想追求低耗电，那应该开启少量的规则，由于之前的默认规则数量有 1300+，很多人喜欢无脑开启规则

开启这么多规则，并且在这些规则匹配的界面使用手机，不耗电是不可能的

此外，某些软件如抖音的无障碍节点数量比较多，并且产生无障碍事件频率也比较高

长时间下使用此类软件的规则会比较耗电，请自行考虑后再启用

## 未识别应用 {#unknown-app}

某些用户可能选择将应用安装到其他用户空间隔离

这导致 GKD 无法从当前应用列表识别到应用已安装

对于未安装的应用, 有以下影响

- 全局规则 的内部配置禁用失效
- 应用规则 不会启用

对于 `全局规则` 可使用手动编辑禁用, 添加 appId 到禁用列表后将生效

若要开启 `应用规则`, 在对应订阅-应用规则-显示未安装应用-打开右侧开关即可

::: details 不生效原因
这是因为某些订阅有将近 2k 个应用, 而一般用户最多使用到 200 个

如果将 未安装的应用 的应用规则也全部开启, 这将额外占用 1800 个应用的无效规则配置内存
:::

## 后台运行 {#persistent}

如何尽量保持后台运行不被系统回收

- 任务切换界面给 GKD 应用卡片加锁即可

一般情况下, 使用此项即可正常后台运行, 如果不行请使用下面的步骤

- 打开 GKD 首页, 开启 `常驻通知`
- 打开 GKD 设置, 开启 `后台隐藏`
- 允许后台活动, 关闭省电策略, 或者设置 GKD 的省电策略为无限制
- 允许 GKD 自启动

## 受限制的设置 {#restriction}

> [!TIP] 建议
> 授予 `写入安全设置权限` 后可自行开启无障碍, 而无需设置此项

无障碍列表界面提示 `受限制的设置(出于安全考虑，此设置目前不可用)`

这是 Android13 的限制, 对于不在应用商店等可信任来源安装的应用不能直接开启无障碍权限

您需要解除这个限制, 到系统设置-应用管理-找到并点击GKD-右上角-允许受限制的设置

以 LineageOS 20 为例, 下面为完整的解除限制流程截图, 此处感谢来自 [CyrusYip](https://github.com/gkd-kit/docs/issues/2) 的截图

<ImageTable :images="[['0013.png', '0014.png', '0015.png', '0016.png'], ['0017.png', '0018.png']]" />

如果您按照以上步骤设置后回到 无障碍列表 仍然提示不可用, 您可以试试 **重启手机**, 此解决方案来自 [Herobrine2005928](https://github.com/orgs/gkd-kit/discussions/433#discussioncomment-8899920)

## 关闭无障碍警告弹窗 {#close_warn_dialog}

> [!TIP] 建议
> 授予 `写入安全设置权限` 后可自行开启无障碍, 而无需设置此项

这个方案不一定适用所有机型

大多数设备开启无障碍时都会出现 10s 的无障碍警告弹窗

若是只需要开启一次则无所谓但是如果开启次数比较多每次都有这个警告等待就很烦人了

<ImageTable :images="[['0004.png', '0005.png']]" />

你可能已经看到这个界面还有一个开关, 也就是下方的 `快捷方式` 开关

打开一次下面这个快捷方式开关后, 上面的的开启按钮就不会出现警告弹窗了, 但是你会发现屏幕侧边出现了一个应用小图标, 多数情况下我们并不需要这个图标

到无障碍界面-"无障碍"按钮-使用按钮或手势-点击切换为手势即可隐藏

以 Xiaomi HyperOS 为例子, 下面是完整的关闭弹窗流程截图

<ImageTable :images="[['0009.png', '0010.png', '0011.png', '0012.png']]" />

## 手动写入安全设置权限失败 {#fail_setting_secure_settings}

在使用 adb 手动写入安全设置时可能会提示权限不够，具体报错如下:

```text
adb shell pm grant li.songe.gkd android.permission.WRITE_SECURE_SETTINGS

Exception occurred while executing 'grant':
java.lang.SecurityException: grantRuntimePermission: Neither user 2000 nor current process has android.permission.GRANT_RUNTIME_PERMISSIONS.
  at android.app.ContextImpl.enforce(ContextImpl.java:2384)
  at android.app.ContextImpl.enforceCallingOrSelfPermission(ContextImpl.java:2412)
  at com.android.server.pm.permission.PermissionManagerServiceImpl.grantRuntimePermissionInternal(PermissionManagerServiceImpl.java:1383)
  at com.android.server.pm.permission.PermissionManagerServiceImpl.grantRuntimePermission(PermissionManagerServiceImpl.java:1365)
  at com.android.server.pm.permission.PermissionManagerService.grantRuntimePermission(PermissionManagerService.java:573)
  at android.permission.PermissionManager.grantRuntimePermission(PermissionManager.java:610)
  at com.android.server.pm.PackageManagerShellCommand.runGrantRevokePermission(PackageManagerShellCommand.java:2717)
  at com.android.server.pm.PackageManagerShellCommand.onCommand(PackageManagerShellCommand.java:301)
  at com.android.modules.utils.BasicShellCommandHandler.exec(BasicShellCommandHandler.java:97)
  at android.os.ShellCommand.exec(ShellCommand.java:38)
  at com.android.server.pm.PackageManagerService$IPackageManagerImpl.onShellCommand(PackageManagerService.java:6840)
  at android.os.Binder.shellCommand(Binder.java:1092)
  at android.os.Binder.onTransact(Binder.java:912)
  at android.content.pm.IPackageManager$Stub.onTransact(IPackageManager.java:4352)
  at com.android.server.pm.PackageManagerService$IPackageManagerImpl.onTransact(PackageManagerService.java:6824)
  at android.os.Binder.execTransactInternal(Binder.java:1392)
  at android.os.Binder.execTransact(Binder.java:1299)
```

在开发者选项中找到 `禁止权限监控`，打开后重新运行adb指令即可。
