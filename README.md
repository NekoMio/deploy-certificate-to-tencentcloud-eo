# GitHub Action for Tencent Cloud TEO certificate deployment

Deploy SSL certificate to Tencent Cloud TEO.

## Usage

This action will deploy your PEM-formatted SSL certificate to Tencent Cloud TEO.

```yaml
jobs:
  deploy-to-qcloud-teo:
    name: Deploy certificate to Tencent Cloud TEO
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          # If you just commited and pushed your newly issued certificate to this repo in a previous job,
          # use `ref` to make sure checking out the newest commit in this job
          ref: ${{ github.ref }}
      - uses: NekoMio/deploy-certificate-to-tencentcloud-eo@master
        with:
          # Use Access Key
          secret-id: ${{ secrets.QCLOUD_SECRET_ID }}
          secret-key: ${{ secrets.QCLOUD_SECRET_KEY }}

          # Specify PEM fullchain file
          fullchain-file: ${{ env.FILE_FULLCHAIN }}
          # Specify PEM private key file
          key-file: ${{ env.FILE_KEY }}

          zone-id: zone-xxxxx # Replace with your actual TEO zone ID

          # Deploy to CDN
          zone-id-domains: |
            cdn1.example.com
            cdn2.example.com
```

## Permissions

Please make sure the Tencent Cloud account you use has the following permissions:

- QcloudTEOFullAccess
- QcloudSSLFullAccess
