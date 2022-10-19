Run in powershell to deploy:
```pws
$templateFile = "./template.json"
$parameterFile="./parameters.json"
$resourceGroupName="positive-matching-demo-dev"
New-AzResourceGroup `
  -Name $resourceGroupName `
  -Location "westeurope"
$Resources = New-AzResourceGroupDeployment `
  -ResourceGroupName $resourceGroupName `
  -TemplateFile $templateFile `
  -TemplateParameterFile $parameterFile
```

Add "FHIR Data Reader" Rule for the created webapp:

```pws
New-AzRoleAssignment -ObjectId $Resources.outputs.webappObjectId.Value ` 
 -RoleDefinitionName "FHIR Data Reader" `
 -Scope <fhir server resource ID>
```