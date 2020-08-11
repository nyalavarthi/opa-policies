# opa-policies
Evaluate terraform code for compliance and security policies using OPA and Regula. 


1. terraform init
2. terraform plan --out tfplan.binary
3. terraform show -json tfplan.binary > tfplan.json
4. opa eval --format pretty --data s3-validate.rego --input tfplan.json "data.terraform.analysis.score"
5. opa eval --format pretty --data s3-validate.rego --input tfplan.json "data.terraform.analysis.authz"
6. opa eval -f pretty --explain=notes  --data rds-validate.rego --input tfplan.json "authorized = data.terraform.analysis.authz; violations = data.terraform.analysis.violation"
