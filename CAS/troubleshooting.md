# Trouble Shooting 

SAP Cloud Application Studio(CAS) Trouble Shooting 

# BC set not assigned to a Business Option

## Symptom

Solution Assemble Failed.

```
Auto adjust not possible as there more than one Business Options. 
Open BAC to assign content
```

## Cause

BAC 오브젝트에 BO 미할당

솔루션에 새로운 CBO가 생성되면 BAC에 새로 할당해주어야 함

## Resolution

1. Open BAC 
2. Assign Solution Content

https://userapps.support.sap.com/sap/support/knowledge/en/2913894

## Merge the change project 

If a BC change project is open on the tenant before you enable the patch solution on the test tenant, you will not be able to merge the change project unless you disable the patch solution

Merge of a Change Project is copying the configuration data (Scoping and Fine Tuning) from the Change Project to the Productive project. Before merge, all the activities of the Change Project have been completed.

주의 ) 솔루션 Disable 시, 구현 프로젝트 > 범위 설정과 액티비티가 초기화 된다.

https://blogs.sap.com/2015/09/08/change-project-merge-and-sync-with-production/