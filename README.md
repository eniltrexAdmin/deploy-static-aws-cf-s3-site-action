# Deploy React Static Site Github Action (AWS CF + S3)

A github action to deploy a static site hosted on AWS with Cloudfront and S3 as backend.

You may check the action.yml to know more concisely what it does.

Basically execute the npm run build to create the deployable files and then syncs those.




## Usage

Use this action like this to deploy automatically:


```yaml
  deploy-production:
    runs-on: ubuntu-latest
    steps:
      - id: Deploy Site
        uses: eniltrexAdmin/deploy-static-aws-cf-s3-site-action@v1.0.1
        with:
          aws-access-key-id: ${{ secrets.AWS_DEPLOYER_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_DEPLOYER_KEY_SECRET }}
          aws-region: eu-west-3
          aws-s3-bucket-name: ${{ secrets.AWS_S3_BUCKET_NAME }}
          aws-cf-id: ${{ secrets.AWS_CF_ID }}
```

## Variables

All 5 env variables that oyu see above in the usage are required. I hope the name is self
explanatory.

## Cloudfront and S3 structure

I don't know exactly why, but in my last company we would separate the "assets" to have a different
origin. For a static site, that's pretty much everything, all the JS CSS and even pictures etc.
(I would say the main reason was something about caching more strongly or something like that).

I followed though the same structure. Therefore, it is expected that CF has two origins,
the main one and the public that points to the s3 directory /public, and everything is inside that
except the main index.html.

I would say that is kind of a custom behaviour, so you are free to do forks, PR or just copy and 
customize the action according to your needs.
