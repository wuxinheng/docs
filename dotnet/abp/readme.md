# abp 

> 这份文档的意义旨再更详细介绍abp框架的时候



## 依赖注入

> 个人认为学习到此处一定需要对.net core的生命周期了解到位这个是前提。这个官方文档相比其他描述好懂很多。
>
> 详见[Dependency-Injection.md](/Dependency-Injection.md)

### .net core ioc

#### 权重

AddSingleton→AddTransient→AddScoped

#### 生命周期

项目启动-项目关闭   相当于静态类  只会有一个  

AddScoped的生命周期：

请求开始-请求结束  在这次请求中获取的对象都是同一个 

AddTransient的生命周期：

请求获取-（GC回收-主动释放） 每一次获取的对象都不是同一个



## API

### 自动api控制器

**必要条件**：`Application` 项目中的 `Service` 必须实现`IApplicationService`

**规范**：`Application.Contracts` 项目定义`Application`中`Service`需要实现的接口，接口可以直接实现`IApplicationService`

**具体操作**：在`Application`项目中`ApplicationModule`类`ConfigureServices`方法加入以下代码

> 并不是ApplicationModule.cs，是与实际项目中*ProjectName*ApplicationModule.cs,下面代码也是如此。

```c#
Configure<AbpAspNetCoreMvcOptions>(options =>
        {
            options
                .ConventionalControllers
                .Create(typeof(ApplicationModule).Assembly);
        });
```

### 动态C# API客户端

**必要条件**：在`xblogs.HttpApi.Client`项目中`AbpModule`派生类`ConfigureServices`方法中加入以下代码：

> 并不是ApplicationContractsModule.cs，是与实际Application.Contracts项目中*ProjectName*ApplicationContractsModule.cs,下面代码也是如此。

```C#
// 创建动态客户端代理
context.Services.AddHttpClientProxies(
     typeof(ApplicationContractsModule).Assembly
);
```

**具体操作**：`xblogs.HttpApi`项目中正常写控制器，正常开发就可以了。

## MailKit

1、在`Domain`模块使用设置系统来进行配置：继承`SettingDefinitionProvider`重写`Define`方法更具文档上添加需要的信息。

```
public class xblogsSettingDefinitionProvider : SettingDefinitionProvider
{
    public override void Define(ISettingDefinitionContext context)
    {
        // Eail Setting Infomation
        context.Add(new SettingDefinition(EmailSettingNames.Smtp.Host, "smtp.qq.com"),
                new SettingDefinition(EmailSettingNames.Smtp.Port, "465"),
                new SettingDefinition(EmailSettingNames.Smtp.UserName, "934041144@qq.com"),
                new SettingDefinition(EmailSettingNames.Smtp.Password, "12345"),
                new SettingDefinition(EmailSettingNames.Smtp.Domain),
                new SettingDefinition(EmailSettingNames.Smtp.EnableSsl, "true"),
                new SettingDefinition(EmailSettingNames.Smtp.UseDefaultCredentials, "false"),
                new SettingDefinition(EmailSettingNames.DefaultFromAddress, "934041144@qq.com"),
                new SettingDefinition(EmailSettingNames.DefaultFromDisplayName, "xblogs"));

    }
}
```

2、在`Domain`模块新建模块。

```
    /// <summary>
    /// MailKit模块
    /// </summary>
    [DependsOn(
    typeof(AbpMailKitModule)
    )]
    public class MailKitModule : AbpModule
    {
        public override void ConfigureServices(ServiceConfigurationContext context)
        {

            Configure<AbpMailKitOptions>(options =>
            {
                options.SecureSocketOption = SecureSocketOptions.SslOnConnect;
            });

        }

    }
```

3、在`DomainModule`注册我们的`MailKitModule`

```
[DependsOn(
    typeof(MailKitModule)
)]
public class xblogsDomainModule : AbpModule
{
    public override void ConfigureServices(ServiceConfigurationContext context)
    {
        Configure<AbpMultiTenancyOptions>(options =>
        {
            options.IsEnabled = MultiTenancyConsts.IsEnabled;
        });
    }
}
```

> 这里有个概念非常好模块化。我在这里纠结了很长时间abp理念是模块化，减少冗余。可以简单理解为拼积木。请看`模块化`
>
> 我当然非常愿意学习一个东西时先看文档。但是文档这个东西很难说每个人的理解能力也不一样。我没有看懂abp这一块的文档。我就直接上手操作。不对就换方法。当自己的摸索出来了之后就可以跟着自己的理解去看文档和写代码了。

## 模块化

概念：简单来说模块化就是将功能拆分，需要用的时候拿来用。

abp中的模块：我是这么理解我将框架基础功能的配置拆分在不同模块中，但这个也是根据不同的需求和场景来完成的。我们可以将功能模块化配置的尽可能的零散些。在Application 中我们可以新建模块，不同的模块注入不同的功能模块类。再将自己的新建的模块类注入到ApplicationModule中，这里需要的注意的是ApplicationModule中默认注入了DomainModule。所以在配置MailKit时只是注入了MailKitModule。我在实现邮件功能的时候也尝试将MailKitModule写在Application项目中。但是出现错误。我觉得可能是注入的问题，我就选择写在Domain项目中。这里其实还可以再去钻研的。ApplicationModule是整个程序的主入口。他就像个大水池不断有水流入。我就把ApplicationModule中的内容清空了，让这个类主要来负责程序的注入。
