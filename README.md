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

    ```aws s3 sync --exclude '*' --include '*index.html*' . s3://docs.zeff.ai/```

* Commit changes. 
* Party.

#### Invalidate the Cloudfront cache
Unfortunately, you can make changes and they'll be noticed find in the S3 bucket but if the site is fronted by Cloudfront, the old files will still be in the cache. 

So you're going to have to invalidate the cache and wait a Kearney, Nebraska minute (These take longer because a) people in Kearney, NB move slower, and b) time slows down whenever an wherever you are in NB.) 

i.e. Cloudfront invalidates at a near glacial pace. 

So to invalidate, get the distribution id:


```aws cloudfront list-distributions```

And find the distribution id for the docs.zeff.ai S3 bucket.

Then invalidate the cache:

```aws cloudfront create-invalidation --distribution-id=<you found this id in the previous command - insert it here> --paths=/```

Then wait. For about....a Kearney, NB minute and then check your website links again. 

Maybe I'll do a script for that does this if you're nice to me. Or if you bring me a doughnut, which is pretty much the same thing.