---
title: Uploading files to Amazon S3 from Mac OSX terminal
layout: post
---

Sign in to Amazon AWS and get [access
credentials](https://portal.aws.amazon.com/gp/aws/securityCredentials?#access_credentials).
Then install and configure [s3cmd](http://s3tools.org/s3cmd) as follow.

{% highlight bash %}
$ sudo port install gnupg
$ sudo port install s3cmd
$ s3cmd --configure
{% endhighlight %}

* List contents: `s3cmd ls`, `s3cmd ls s3://bucket_name`
* Upload a file and make public: `s3cmd -P put /path/to/local/file.ext s3://bucket_name/remote/path/file.ext`

{% highlight bash %}
$ s3cmd -h

Commands:
  Make bucket
      s3cmd mb s3://BUCKET
  Remove bucket
      s3cmd rb s3://BUCKET
  List objects or buckets
      s3cmd ls [s3://BUCKET[/PREFIX]]
  List all object in all buckets
      s3cmd la
  Put file into bucket
      s3cmd put FILE [FILE...] s3://BUCKET[/PREFIX]
  Get file from bucket
      s3cmd get s3://BUCKET/OBJECT LOCAL_FILE
  Delete file from bucket
      s3cmd del s3://BUCKET/OBJECT
  Synchronize a directory tree to S3
      s3cmd sync LOCAL_DIR s3://BUCKET[/PREFIX] or s3://BUCKET[/PREFIX] LOCAL_DIR
  Disk usage by buckets
      s3cmd du [s3://BUCKET[/PREFIX]]
  Get various information about Buckets or Files
      s3cmd info s3://BUCKET[/OBJECT]
  Copy object
      s3cmd cp s3://BUCKET1/OBJECT1 s3://BUCKET2[/OBJECT2]
  Move object
      s3cmd mv s3://BUCKET1/OBJECT1 s3://BUCKET2[/OBJECT2]
  Modify Access control list for Bucket or Files
      s3cmd setacl s3://BUCKET[/OBJECT]
  Enable/disable bucket access logging
      s3cmd accesslog s3://BUCKET
  Sign arbitrary string using the secret key
      s3cmd sign STRING-TO-SIGN
  Fix invalid file names in a bucket
      s3cmd fixbucket s3://BUCKET[/PREFIX]
  List CloudFront distribution points
      s3cmd cflist
  Display CloudFront distribution point parameters
      s3cmd cfinfo [cf://DIST_ID]
  Create CloudFront distribution point
      s3cmd cfcreate s3://BUCKET
  Delete CloudFront distribution point
      s3cmd cfdelete cf://DIST_ID
  Change CloudFront distribution point parameters
      s3cmd cfmodify cf://DIST_ID

{% endhighlight %}

References:

* [Install s3cmd tools on a Mac OSX for Amazon S3](http://devsforrest.com/4/install-s3cmd-tools-on-a-mac-os-x-for-amazon-s3-bucket-access-upload-sync-etc)
* [Git push to Amazon S3](http://stackoverflow.com/questions/5187496/git-push-to-amazon-s3-for-deploying-assets)
* [s3cmd](http://s3tools.org/s3cmd)
