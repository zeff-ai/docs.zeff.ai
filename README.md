### Zeff static docs site.

The Zeff client and server API documentation lives in Zeff S3 and is
hosted on docs.zeff.ai.

This has been done as a static AWS site, which means there is a CloudFront
distribution with certs fronting the S3 docs.zeff.ai bucket - aliased 
in route53, all under the Zeff AWS account.

This repo is solely for maintaining the directory structure and not much else.
The zeffclient docs are currently uploaded and published to the bucket with
a "make publish" in the documentation source for zeffclient.

Zeffserver will also follow this pattern (got that?!). For the moment, this repo contains
a zeffserver/index.html as a placeholder for when the server part of Zeff is
open sourced.

To make any changes to the site (It's pretty, umm, sparse).
* Check out this repo.
* Change/fix anything in index.html at the head of the git repo.
* Sync to aws from this dir with:

    `aws s3 sync --exclude '*' --include '*index.html*' . s3://docs.zeff.ai/`

* Commit changes. 
* Party.
