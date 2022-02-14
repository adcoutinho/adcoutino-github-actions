# adcoutino-github-actions


The purpose of this repo is to archive Github Actions workflows examples:

*terraform-apply.yml* - Simple ``` terraform apply``` workflow for AWS triggered when a push to main happens with output inside PR;

*terraform-destroy.yml* - Simple ``` terraform destroy``` workflow for AWS triggered when a push to main happens with output inside PR;

*terraform-destroy.yml* - Simple ``` terraform plan``` workflow for AWS triggered when a push to main happens with output inside PR;


In order to use those actions you should:

1 - Create ```.github\workflows folder``` inside the root of repo;

2 - Change environment parameters directly to each file or create Environments and Secrets in Github Settings to reference here:
```
matrix:
        environment:
          - name: xxxxxxxxx
            aws_account_id: xxxxxxxxx
            aws_region: xxxxxxxxx
            terraform_version: 1.0.1
```


3 - Change those parameters with direct input or Env Secrets too:
```
env:
      AWS_ACCOUNT_ID: ${{ matrix.environment.aws_account_id }}
      AWS_REGION: xxxxxxxxx
      ENVIRONMENT: ${{ matrix.environment.name }}
      TF_WORKDIR: xxxxxxxxx
```

*TF_WORKDIR* must be the place where Terraform files resides.


4 - For AWS Credentials it must be Env Secrets for security reason in this case **AWS_ACCESS_KEY** and **AWS_SECRET_ACCESS_KEY**:
```
- name: Configure AWS Credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```
