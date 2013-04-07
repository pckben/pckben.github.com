---
title: Hosting a static website on Amazon S3 with naked domain name.
layout: post
---
So I've been looking for a quick and cheap way to write web applications that is
fast and highly scalable. Today I hacked together my first app,
[my24.me](http://my24.me), which lets you plan, log down and track what you do
with your 24 hours each day. If you ever thought that 24 hours a day seems not
enough, then perhaps you should check it out. Anyway, here are the methods and
services I used:

## 1. Firebase as backend

[Firebase](https://www.firebase.com) is a nice way to get rid of server side
coding completely if all you need is a backend that provide methods to access
your data objects from JavaScript client code. Although not tested, Firebase is
advertised as highly scalable. At $1/month, its pricing is _very_ affordable,
too. There are a lot of alternatives to Firebase, too:
[PubNub](http://www.pubnub.com), [Parse](https://parse.com),
[mongolab](https://mongolab.com), [Amazon
DynamoDB](http://aws.amazon.com/dynamodb/). I haven't tried out any of them, but
it seemed to me at the first glance that Firebase is a winner in terms of
pricing, scalability and ease of use.

## 2. Amazon S3 as static website hosting

Hosting on [Amazon S3](http://aws.amazon.com/s3/) is [really
cheap](http://aws.amazon.com/s3/pricing/): at $0.09/GB/month. My webapp is never
gonna need more than a GB storage, so it's about $1/year hosting!

## 3. Amazon Route 53 to allow naked domain

[Amazon Route 53](http://aws.amazon.com/route53/) recently lets naked domains
(such as [my24.me](http://my24.me)) to be served from an Amazon S3 bucket. This is
an amazing feature as it not only allow your website to be advertised with a
clean, www-less domain, but also prevent various [potential
problems](https://devcenter.heroku.com/articles/avoiding-naked-domains-dns-arecords)
associated with using a naked domain, if it is configured as redirecting to its
www subdomain using free services such as [wwwizer.com](http://wwwizer.com/).
The details on configuring Amazon S3 and Route 53 is
[here](http://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html).

## 4. Deploying with `s3cmd`

Using git and the [`s3cmd`
tool](/2013/04/07/mac-osx-uploading-files-to-amazon-s3/), we can have out
website developed in a private git repository, such as
[BitBucket](https://bitbucket.org/), and then pushes the production branch to
Amazon S3 automatically. Below is the command to sync your local production
directory with an S3 bucket. You can also set up a git hook to sync this
directory automatically for continuous deployment.

{% highlight bash %}
s3cmd sync \
  --recursive \
  --acl-public \
  --exclude '.git*/*' \
  --exclude '*.swp' \
  --exclude 'Makefile' \
  /path/to/local/dir \
  s3://path/to/remote/bucket
{% endhighlight %}
