# K8s Deployment action

This repository presents a GitHub Actions step to deploy kubernetes yaml files.

## Example

The following example deploys a template deploy replacing `{{ IMAGE }}` and `{{ TAG }}` in the deployment file.


```yaml
- id: 'auth'
  uses: 'google-github-actions/auth@v0'
  with:
    credentials_json: '${{ secrets.GCP_CREDENTIALS }}'
    token_format: 'access_token'

- name: Deploy
  uses: anthorteam/K8s-Deployment@main
  env:
    IMAGE: gcr.io/anthor-dev/myimage
    TAG: 0000001
  with:
    K8S_NAMESPACE: 'dev'
    DEPLOYMENT_FILE: 'deploy/deploy.yaml'
    DEPLOYMENT_TYPE: 'deployment'
    DEPLOYMENT_NAME: 'test-deploy'
    ROLLOUT_TIMEOUT_MINUTES: '1'
    GKE_CLUSTER: ${{ secrets.GKE_CLUSTER }}
    GKE_CLUSTER_LOCATION: ${{ secrets.GKE_ZONE }}
```