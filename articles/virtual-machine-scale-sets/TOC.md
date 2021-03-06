# [虚拟机规模集文档](index.yml)

# 概述
## [什么是虚拟机规模集？](overview.md)

# 快速入门
## [在 Azure 门户中创建](quick-create-portal.md)
## [使用 Azure CLI 2.0 创建](quick-create-cli.md)
## [使用 Azure PowerShell 创建](quick-create-powershell.md)
## 使用模板创建
### [Linux 规模集](quick-create-template-linux.md)
### [Windows 规模集](quick-create-template-windows.md)

# 教程
## 1 - 创建/管理规模集
### [Azure CLI 2.0](tutorial-create-and-manage-cli.md)
### [Azure PowerShell](tutorial-create-and-manage-powershell.md)
## 2 - 使用数据磁盘
### [Azure CLI 2.0](tutorial-use-disks-cli.md)
### [Azure PowerShell](tutorial-use-disks-powershell.md)
## 3 - 使用自定义 VM 映像
### [Azure CLI 2.0](tutorial-use-custom-image-cli.md)
### [Azure PowerShell](tutorial-use-custom-image-powershell.md)
## 4 - 将应用部署到规模集
### [Azure CLI 2.0](tutorial-install-apps-cli.md)
### [Azure PowerShell](tutorial-install-apps-powershell.md)
### [模板](tutorial-install-apps-template.md)
## 5 - 自动缩放规模集
### [Azure CLI 2.0](tutorial-autoscale-cli.md)
### [Azure PowerShell](tutorial-autoscale-powershell.md)
### [模板](tutorial-autoscale-template.md)
## 使用自定义 Packer 映像将应用部署到 Azure 虚拟机规模集
### [Azure CLI 2.0](https://docs.microsoft.com/learn/deploy-custom-vmss-app/index)

# 示例
## [Azure CLI 2.0](cli-samples.md)
## [PowerShell](powershell-samples.md)

# 如何
## 规划和设计
### [设计注意事项](virtual-machine-scale-sets-design-overview.md)
### [了解实例 ID](virtual-machine-scale-sets-instance-ids.md)

## 创建模板
### [了解规模集模板](virtual-machine-scale-sets-mvss-start.md)
### [使用现有虚拟网络](virtual-machine-scale-sets-mvss-existing-vnet.md)
### [使用自定义映像](virtual-machine-scale-sets-mvss-custom-image.md)
### [将基于来宾的自动缩放与 Linux 规模集模板配合使用](virtual-machine-scale-sets-mvss-guest-based-autoscale-linux.md)

## 部署
### [使用 Visual Studio 进行创建](virtual-machine-scale-sets-vs-create.md)
### [使用可用性区域](virtual-machine-scale-sets-use-availability-zones.md)
### [自动缩放规模集](virtual-machine-scale-sets-autoscale-overview.md)
#### [使用 Azure 门户](virtual-machine-scale-sets-autoscale-portal.md)
#### [高级自动缩放](../monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets.md)
### [规模集中的应用程序](virtual-machine-scale-sets-deploy-app.md)
### [将数据磁盘与规模集配合使用](virtual-machine-scale-sets-attached-disks.md)
### 加密规模集中的磁盘
#### [使用 PowerShell](virtual-machine-scale-sets-encrypt-disks-ps.md)
#### [使用 Azure CLI 2.0](virtual-machine-scale-sets-encrypt-disks-cli.md)
### [使用大型规模集](virtual-machine-scale-sets-placement-groups.md)
### [将规模集模板转换为使用托管磁盘](virtual-machine-scale-sets-convert-template-to-md.md)
### [使用低优先级](virtual-machine-scale-sets-use-low-priority.md)

## 管理
### 常见管理任务
#### [使用 Azure CLI 2.0](virtual-machine-scale-sets-manage-cli.md)
#### [使用 Azure PowerShell](virtual-machine-scale-sets-manage-powershell.md)
### [规模集中的垂直缩放](virtual-machine-scale-sets-vertical-scale-reprovision.md)
### [自动 OS 升级](virtual-machine-scale-sets-automatic-upgrade.md)
### [修改规模集](virtual-machine-scale-sets-upgrade-scale-set.md)
### [使用 DSC 和规模集](virtual-machine-scale-sets-dsc.md)
### [规模集网络](virtual-machine-scale-sets-networking.md)
### [将模板转换为托管磁盘](virtual-machine-scale-sets-convert-template-to-md.md)

## 故障排除
### [自动缩放](virtual-machine-scale-sets-troubleshoot.md)

## 常见问题
### [规模集常见问题](virtual-machine-scale-sets-faq.md)

# 引用
## [Azure PowerShell](/powershell/azure/overview)
## [Azure CLI](../virtual-machines/azure-cli-arm-commands.md)
## [REST](/rest/api/virtualmachinescalesets/)

# 资源
## [Azure 路线图](https://azure.microsoft.com/roadmap/?category=compute)
## 定价 
### [Linux](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/)
### [Windows](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/windows/)
## [定价计算器](https://azure.microsoft.com/pricing/calculator/)
## [堆栈溢出](http://stackoverflow.com/questions/tagged/azure-vm-scale-set)
