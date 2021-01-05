# TDOS 概况

## 简介
&#160;&#160;&#160;&#160;&#160;&#160;TDOS（Trusted Data Operation System）又称可信数据操作系统，是由上海财经大学金融科技研究院和常州市勇阳信息技术有限公司联合研发的全球首款操作系统级区块链服务，包含一整套区块链底层系统、智能合约应用程序的开发与运维技术框架及其衍生服务。 
    
&#160;&#160;&#160;&#160;&#160;&#160;TDOS以快捷部署为核心特点，旨在让一般技术人员和用户能够快速上手开发、自由配置、轻松使用区块链业务系统，打通区块链与一般技术人员、大众间的技术壁垒、认知壁垒，实现区块链应用的加速落地。 

## 未来规划

&#160;&#160;&#160;&#160;&#160;&#160;TDOS产品的版本迭代计划如下：

&#160;&#160;&#160;&#160;&#160;&#160;1）版本号：v2.0

&#160;&#160;&#160;&#160;&#160;&#160;时间：2020年12月

&#160;&#160;&#160;&#160;&#160;&#160;TDOS初步集成版：TDOS基础技术栈及生态工具，一键部署安装区块链底层系统。

&#160;&#160;&#160;&#160;&#160;&#160;2）版本号：v3.0

&#160;&#160;&#160;&#160;&#160;&#160;预计时间：2021年6月

&#160;&#160;&#160;&#160;&#160;&#160;TDOS隐私计算版本：TDOS增强对隐私保护的功能，比如同态隐藏、多方计算、数据重铸等。

&#160;&#160;&#160;&#160;&#160;&#160;3）版本号：v4.0

&#160;&#160;&#160;&#160;&#160;&#160;预计时间：2021年12月

&#160;&#160;&#160;&#160;&#160;&#160;TDOS网中网版本：支持基于TDOS部署的不同的网络跨链及网络合并。

&#160;&#160;&#160;&#160;&#160;&#160;4）版本号：v5.0

&#160;&#160;&#160;&#160;&#160;&#160;预计时间：2022年6月

&#160;&#160;&#160;&#160;&#160;&#160;TDOS全生态工具版本：彻底与操作系统完全集成，软硬件集合，实现可信计算环境。

&#160;&#160;&#160;&#160;&#160;&#160;5）版本号：v6.0

&#160;&#160;&#160;&#160;&#160;&#160;预计时间：2022年12月

&#160;&#160;&#160;&#160;&#160;&#160;TDOS行业集成版：根据不同的业务环境，比如金融、溯源、游戏等，提供定制版本。

## TDOS安装说明

### 部署环境要求

（1）硬件标准

 &nbsp;&nbsp; CPU i5以上；

 &nbsp;&nbsp; 内存：16G运行内存以上；

 &nbsp;&nbsp; 硬盘容量：100G以上；

 (2) 软件标准

  &nbsp;&nbsp; 初始系统环境Mac OS 10.15 以上 / Windows 10以上；

  &nbsp;&nbsp; 本系统以在虚拟机环境下安装为例，也可以在实体机中安装；

  &nbsp;&nbsp; 虚拟机VMWare具体配置要求见附件1；

  &nbsp;&nbsp;（如果没有安装虚拟机可前往官网下载：
 https://www.vmware.com）

  &nbsp;&nbsp;本系统已安装Vmware-tools，如果有需要，可以尝试手动安装，虚拟机VMWare工具安装见附件2；

### TDOS操作系统安装

（1）在虚拟机中安装TDOS.iso镜像；

（2）具体安装步骤：

 &nbsp;&nbsp;第一步：打开虚拟机

![图片1](./img/install/picture1.png)

 &nbsp;&nbsp;第二步：选择Boot system installer，运行TDOS虚拟机镜像系统

![图片2](./img/install/picture2.png)

 &nbsp;&nbsp;第三步：进入默认用户账号（yongyang），输入密码123456（默认），解锁系统后点击sign in 重新设置账号；

![图片3](./img/install/picture3.png)

 &nbsp;&nbsp;第四步：依次填充你的名字、新的用户登录名、用户密码（牢记，后续操作会使用）、Root账户密码(可忽略)以及主机名称（数字英文随意，无字数要求）。完成后，点击进入下一步。

![图片4](./img/install/picture4.png)

 &nbsp;&nbsp;第五步：删除原有分区
 
 ![图片5](./img/install/picture5.png)

 &nbsp;&nbsp;第六步：选择第二个分区，点击箭头（确认）

![图片6](./img/install/picture6.png)

 &nbsp;&nbsp;第七步：勾选方框内容，然后红箭头处选 / 。完成后，点击Next；

![图片7](./img/install/picture7.png)

 &nbsp;&nbsp;第八步：点击start，等待完成

![图片8](./img/install/picture8.png)

![图片9](./img/install/picture9.png)

 &nbsp;&nbsp;第九步：点击reboot；

![图片10](./img/install/picture10.png)

 &nbsp;&nbsp;第十步：如果长时间未进入此界面，点击回车；

![图片11](./img/install/picture11.png)

 &nbsp;&nbsp;第十一步：输入新的账号密码并重新登录

![图片12](./img/install/picture12.png)

 &nbsp;&nbsp;第十二步：TDOS镜像系统安装完成后，显示此界面。

![图片13](./img/install/picture13.png)

### TDOS链部署向导

（1）准备工作：安装向导工具前，如有需要，可先安装Vmware-tools（详见附件2）

（2）向导工具安装

&nbsp;&nbsp;第一步：点红色箭头指示处打开应用界面；

![图片14](./img/install/picture14.png)

&nbsp;&nbsp;第二步：点击红框内应用图标，开始安装；

![图片15](./img/install/picture15.png)

&nbsp;&nbsp;第三步：打开后如图所示，点击红框内进入安装；

![图片16](./img/install/picture16.png)

&nbsp;&nbsp;第四步：此为TDOS软件安装许可协议，阅读同意后，点击红框内进行下一步；

![图片17](./img/install/picture17.png)

&nbsp;&nbsp;第五步：同意后，显示安装包含组件然后点击“继续”按钮；

![图片18](./img/install/picture18.png)

&nbsp;&nbsp;第六步：输入在虚拟机镜像中设置的管理员密码()，并点击“继续”进入下一步；

![图片19](./img/install/picture19.png)

&nbsp;&nbsp;第七步：复制U盘中序列号文档的序列号粘贴即可，点击“继续”按钮；

![图片20](./img/install/picture20.png)

&nbsp;&nbsp;第八步：分别点击下载节点程序、运维工具两个文件；

![图片21](./img/install/picture21.png)

&nbsp;&nbsp;第九步：安装完成后，点击“继续”按钮；

![图片22](./img/install/picture22.png)

&nbsp;&nbsp;第十步：默认选择“连接到已有网络”，也可以选择创建新的网络，新的网络有模板模式和专家模式两种。选择任意一种网络，点击“继续”，进行下一步；

![图片23](./img/install/picture23.png)

&nbsp;&nbsp;第十一步：点击“部署”按钮，进入下一步；

![图片24](./img/install/picture24.png)

&nbsp;&nbsp;第十二步：等待进度条走完全程即可；

![图片25](./img/install/picture25.png)

&nbsp;&nbsp;第十三步：点击完成结束安装。

![图片26](./img/install/picture26.png)

### 安装完成状态说明

（1）安装完成界面如下：

![图片27](./img/install/picture27.png)

（2）功能说明

&nbsp;&nbsp;账号密码：系统统一分配，用于登录TDOS运维平台；

&nbsp;&nbsp;TDOS运维工具：TDOS运维工具能够帮助用户同步监测链的具体情况，在分叉恢复、卡块监测、导入导出、预警通知以及鉴权设置等方面进行运维调整。

&nbsp;&nbsp;DAPP首页：用户可以通过DAPP更直观的了解TDOS应用场景

&nbsp;&nbsp;智能合约开发环境： 用户可在上面进行智能合约的开发。


### 附件

#### 附件1:

Windows版虚拟机配置

在网上下载VMware虚拟机文件进行安装。

第一步：创建新的虚拟机

![图片57](./img/install/picture57.png)

第二步：默认信息进行下一步；

![图片58](./img/install/picture58.png)

第三步：选择本地镜像文件TDOS.iso，下载链接：https://tdos-store.oss-cn-beijing.aliyuncs.com/TDOS.iso

![图片59](./img/install/picture59.png)

![图片60](./img/install/picture60.png)

第四步：选择客户操作系统 linux和版本Ubuntu

![图片61](./img/install/picture61.png)

第五步：虚拟机命名并选择安装位置

![图片62](./img/install/picture62.png)

第六步：指定磁盘容量大小，设置>=50g

![图片63](./img/install/picture63.png)

第七步：自定义虚拟机硬件，建议内存配置不低于8G，处理器数量不少于4个，网络适配器选择桥接模式，勾选复制物理网络连接状态。

![图片64](./img/install/picture64.png)

![图片65](./img/install/picture65.png)

![图片66](./img/install/picture66.png)

![图片67](./img/install/picture67.png)

第八步：安装完成

![图片68](./img/install/picture68.png)

#### 附件2:

安装Vmware-tools

（1）Vmware-tools主要实现虚拟机和windows之间文件的复制与粘贴功能，便于操作；

（2）安装步骤：

第一步：选择虚拟机，点击“Vmware-tools”进行安装；

![图片69](./img/install/picture69.png)

第二步：红框内的信息提示Vmware-tools已经安装完成；

![图片70](./img/install/picture70.png)

第三步：点击Vmware-tools图标打开工具后选择红框内文件进行复制；

![图片71](./img/install/picture71.png)

第四步：将文件粘贴到桌面；

![图片72](./img/install/picture72.png)

第五步：右击空白桌面，选择 Open Termial进入终端；

![图片73](./img/install/picture73.png)

第六步：在命令行界面，输入 cd Desktop进入桌面路径；

![图片74](./img/install/picture74.png)

第七步：在桌面路径输入 tar zxvf 压缩包的名称，解压压缩包；

![图片75](./img/install/picture75.png)

第八步：输入ls，查看是否有此文件，有代表解压成功；

![图片76](./img/install/picture76.png)

第九步：输入 cd vmware-tools-disrib 命令行，进入解压包；

![图片77](./img/install/picture77.png)

第十步：输入 sudo ./vmware-install.pl ，执行安装命令；

![图片78](./img/install/picture78.png)

第十一步：在箭头指向处输入之前设置的虚拟机密码，然后按回车键。（密码不会显示出来）

![图片79](./img/install/picture79.png)

第十二步：回车后，输入命令yes，表示同意安装vmware-tools；

![图片80](./img/install/picture80.png)

第十三步：输入完YES之后，一直按回车直至下图红框内命令行出现，表示安装完成（同时这个屏幕会扩大至填充完黑色部分）

![图片81](./img/install/picture81.png)

## 如何使用本文档

&#160;&#160;&#160;&#160;&#160;&#160;通过本文档可以获取TDOS的架构详情，以及用户使用TDOS的基本方法。首先，要想成为网络中的节点，需要安装并运行一个TDOS客户端。用户可根据安装步骤自行安装需要的组件。在使用上，TDOS提供从部署可信数据链到智能合约开发的全套工具，提供浏览器以供实时展示关键指标，提供运维工具以维护节点，提供应用广场来展现TDOS的多领域应用场景。用户可根据对应工具的详细说明和使用文档中的步骤详解来进行具体操作。