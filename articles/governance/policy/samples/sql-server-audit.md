---
title: 샘플 - SQL Server 감사 설정 감사
description: 이 샘플 정책 정의는 auditIfNotExists를 사용하여 SQL Server 감사 설정을 감사합니다.
services: azure-policy
author: DCtheGeek
manager: carmonm
ms.service: azure-policy
ms.topic: sample
ms.date: 01/23/2019
ms.author: dacoulte
ms.openlocfilehash: 1e0731de5ce2a12fee6b203f245e42aa4bc67d6e
ms.sourcegitcommit: fcb674cc4e43ac5e4583e0098d06af7b398bd9a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/18/2019
ms.locfileid: "56338175"
---
# <a name="sample---audit-sql-server-audit-settings"></a>샘플 - SQL Server 감사 설정 감사

이 기본 제공 정책은 감사 설정을 사용할지 여부에 따라 SQL Server를 감사합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a>샘플 템플릿

```json
{
  "if": {
    "field": "type",
    "equals": "Microsoft.SQL/servers"
  },
  "then": {
    "effect": "auditIfNotExists",
    "details": {
      "type": "Microsoft.SQL/servers/auditingSettings",
      "name": "default",
      "existenceCondition": {
        "allOf": [
          {
            "field": "Microsoft.Sql/auditingSettings.state",
            "equals": "[parameters('setting')]"
          }
        ]
      }
    }
  }
}
```

[PowerShell](#deploy-with-powershell) 또는 [Azure CLI](#deploy-with-azure-cli)와 함께 [Azure Portal](#deploy-with-the-portal)을 사용하여 이 템플릿을 배포할 수 있습니다. 기본 제공 정책을 가져오려면 ID `a6fb4358-5bf4-4ad7-ba82-2cd2f41ce5e9`를 사용합니다.

## <a name="parameters"></a>매개 변수

매개 변수 값을 전달하려면 다음 형식을 사용합니다.

```json
{"setting": {"value":"enabled"}}
```

## <a name="deploy-with-the-portal"></a>포털을 사용하여 배포

정책을 할당할 경우 사용할 수 있는 기본 제공 정의에서 **SQL Server 수준 감사 설정 감사**를 선택합니다.

## <a name="deploy-with-powershell"></a>PowerShell을 사용하여 배포 

[!INCLUDE [sample-powershell-install](../../../../includes/sample-powershell-install-no-ssh-az.md)]

```azurepowershell-interactive
$definition = Get-AzPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/a6fb4358-5bf4-4ad7-ba82-2cd2f41ce5e9

New-AzPolicyAssignment -name "SQL Audit audit" -PolicyDefinition $definition -PolicyParameter '{"setting": {"value":"enabled"}}' -Scope <scope>
```

### <a name="clean-up-powershell-deployment"></a>PowerShell 배포 정리

정책 할당을 제거하려면 다음 명령을 실행합니다.

```azurepowershell-interactive
Remove-AzPolicyAssignment -Name "SQL Audit audit" -Scope <scope>
```

## <a name="deploy-with-azure-cli"></a>Azure CLI를 사용하여 배포

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy assignment create --scope <scope> --name "SQL Audit audit" --policy a6fb4358-5bf4-4ad7-ba82-2cd2f41ce5e9 --params '{"setting": {"value":"enabled"}}'
```

### <a name="clean-up-azure-cli-deployment"></a>Azure CLI 배포 정리

정책 할당을 제거하려면 다음 명령을 실행합니다.

```azurecli-interactive
az policy assignment delete --name "SQL Audit audit" --resource-group myResourceGroup
```

## <a name="next-steps"></a>다음 단계

- [Azure Policy 샘플](index.md)에서 더 많은 샘플 검토