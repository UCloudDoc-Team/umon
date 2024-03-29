

# 告警模板

## 1.告警模板简介

“告警模板”提供了一种批量设置资源告警的功能。通过预先定义模板中的告警规则，能够将模板与资源以绑定的方式进行结合，将模板中已经定义的规则应用到资源上。



## 2.告警模板基本操作

在告警模板页面中，默认已经为各种资源创建了不同的默认告警模板。使用默认告警模板可以快速的为资源设置基本的告警规则。

![](/images/guide/alarm_template.png)

如用户希望修改或增加更多的告警规则，则可创建或根据默认的告警模板生成或创建新的告警模板。

> 注解：默认告警模板无法修改，如修改后需要保存，请另存为新的自定义告警模板。



点击“创建模板”按钮创建新的告警模板，需要依次选择模板所对应的资源类型（如云主机）、规则导入来源、模板名称及管理备注后，点击创建打开“编辑告警模板”窗口。

![](/images/guide/create_alarm_template.png)

点击“添加规则”下拉按钮，会出现对应资源类型的不同监控指标，下图中选择的是“CPU使用率”，并将告警阈值设置为“95%”，通知对象为“默认组”。点击保存后完成告警模板创建。

![](/images/guide/alarmtemplate_rules.png)

另外，在告警模板列表中，还可以查看到某个模板已经绑定的资源数量，以及具体有哪些资源绑定到了该模板上，并可对现有模板中的规则进行编辑。

> 注释：为资源绑定告警模板，参见 [资源监控的2.4-设置告警](umon/resource.md)
>
