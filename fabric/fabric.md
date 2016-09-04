#Fabric

> [Fabric文档](https://docs.fabric.io/android/fabric/overview.html)


## Crashlytics

![apps](./pic/crashlytics1.png)

Crashlytics页面上可以查看crash概况，并且可以选择特点的Version、event、data

Crash是按`Issue Impact level`      排序的：
![level1](./pic/level1.png) ··· ![level5](./pic/level5.png) ![level6](./pic/level6.png)
## Settings
> APPS、Organizations、Account、Notification

![setting](./pic/setting.png)

### APPS
![apps](./pic/apps.png)

点击“Add”按钮可以添加所要监控的APP，在已添加的APP后面点击“stop watching”按钮可停止发送Crash报告。

而点击对应的APP进入对应的APP详情页。

作为管理员可以有：移除小组成员，修改APP名字，移除不再监控的APP或移除不再监控的APP版本等权限。
### Organizations
![apps](./pic/organizations.png)

在Organizations页面下可以查看加入的Organization，并显示了team的概况，点击对应的Team可以进入详情页。
#### Team Members
![team](./pic/team.png)

在Organization页面下可以查该Organization的API Key与Build Secret，并且管理员可以修改该Organization的name，注意每个Organization的API key与Build Secret值都不一样，都同一个Organization的APP都应该使用同一个API Key。该值需在AndroidManifest.xml文件中配置：
   

	<meta-data  
		android:name="io.fabric.ApiKey"
		android:value="134feb6b0141133aacb12579b08e3fba5b660049" />


当将你所在的Organization的API key设置进AndroidManifest.xml后，你所在的team都可以收到该APP的Crash的报告。
> 例：
> 在Personal的Organization中的API Key值为：147bd5fec620bef21d14ae715e6123d177723a72，
> 此时build之后则在该Organization的APP tab中看到此APP的选项

![apikettest](./pic/apikey_test.png)

此时即可在APP Tab页则会显示出所有该API Key的APP

![apikettest](./pic/apikey_test2.png)

# Notification
在Notification 页面下添加接收提醒的邮箱，并且可以为你所在的组设置不同的邮箱。

![apikettest](./pic/notification.png)

##### 权限
> 在Fabric中有两种权限：Admins and Members.

Admins自动查看organizations下所有的APP，并且能够:

- 更改team成员的权限
- 更改organization设置
	- 编辑organization的名称
	- 删除organization
	- 邀请或是移除team成员
- 更改app设置
	- 在Beta or Crashlytics下禁用或启用APP版本
	- 编辑app的名称
	- 增加team成员
	- 删除apps
	- 增加service hooks
- 接收notifications

Members只可以拥有apps的部分权限:

- 更改app设置
	- 增加service hooks
	- 增加team成员
- 接收notifications

### Debug包与Realease包
- 为Debug与Realease设置不一样的包名

在gradle中配置：

    buildTypes {  
        debug{
            applicationIdSuffix ".debug"
        }

配置完成build之后，在fabric上会显示两个APP，debug包名有.debug后缀

- 为Debug与Realease设置不同的notifications，使用不同的API Key