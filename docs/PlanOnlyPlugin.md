## [PlanOnlyPlugin](../src/PlanOnlyPlugin.groovy)

Enable this plugin to add a parameter to the build which will restrict pipeline functionality to `terraform plan` only.

```
// Jenkinsfile
@Library(['terraform-pipeline@v3.10']) _

Jenkinsfile.init(this, env)

// This enables the "plan only" functionality
PlanOnlyPlugin.init()

def validate = new TerraformValidateStage()

def destroyQa = new TerraformEnvironmentStage('qa')
def destroyUat = new TerraformEnvironmentStage('uat')
def destroyProd = new TerraformEnvironmentStage('prod')

validate.then(destroyQa)
        .then(destroyUat)
        .then(destroyProd)
        .build()
```
