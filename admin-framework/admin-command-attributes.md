---
title: 管理员命令属性
description: 在插件中使用管理员命令属性的指南
icon: Shield
---

## 为命令分配权限

为命令分配权限非常简单，只需在命令方法（函数回调）上标记RequiresPermissions或RequiresPermissionsOr属性即可。这两个属性之间的区别在于RequiresPermissionsOr只需要调用者拥有列出的权限之一即可通过，而RequiresPermissions需要调用者拥有所有列出的权限。CounterStrikeSharp会在后台为您处理所有的权限检查。

```csharp
[RequiresPermissions("@css/slay", "@custom/permission")]
public void OnMyCommand(CCSPlayerController? caller, CommandInfo info)
{
    ...
}
```

```csharp
[RequiresPermissionsOr("@css/ban", "@custom/permission-2")]
public void OnMyOtherCommand(CCSPlayerController? caller, CommandInfo info)
{
    ...
}
```

甚至可以将这些属性堆叠在一起，所有属性都会被检查。

```csharp
// Requires (@css/cvar AND @custom/permission-1) AND either (@custom/permission-1 OR @custom/permission-2).
[RequiresPermissions("@css/cvar", "@custom/permission-1")]
[RequiresPermissionsOr("@css/ban", "@custom/permission-2")]
public void OnMyComplexCommand(CCSPlayerController? caller, CommandInfo info)
{
    ...
}
```

您也可以使用相同的属性来检查组。

```csharp
[RequiresPermissions("#css/simple-admin")]
public void OnMyGroupCommand(CCSPlayerController? caller, CommandInfo info)
{
    ...
}
```

