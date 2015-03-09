---
title: "avoid cross domain issue when serving assets from AWS S3 + Cloudfront"
layout: "post"
permalink: "/2015/03/avoid-cross-domain-issue-for-s3-cloudfront.html"

---

**Problem**

I have been facing a browser cross domain problem for a while. I have my asset file stored in AWS S3 and use cloudfront as CDN. The problem is the font file is blocked by browser, Chrome keeps reporting error ***"has been blocked from loading by cross-origin resource sharing policy"*** as show in screenshot below:

![Browser block font file][browser_error]

**Solution**

I did some search on internet and found out this [this article][1] So I need to explicitely config Cross-origin resource sharing (CORS) rule for my S3 bucket.

- From AWS S3 console, click the bucket you want to enable CORS rule, then click "Properties" -> "Permissions" -> "Edit CORS Configuration"

![Edit CORS Configuration][s3_1]

- In the form, set your CORS rules as follows:


		<?xml version="1.0" encoding="UTF-8"?>
			<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
		    <CORSRule>
		        <AllowedOrigin>[set allowed domain here]</AllowedOrigin>
		        <AllowedMethod>GET</AllowedMethod>
		        <MaxAgeSeconds>3000</MaxAgeSeconds>
		        <AllowedHeader>*</AllowedHeader>
		    </CORSRule>
		</CORSConfiguration>

![Edit CORS Configuration 2][s3_2]

This setting will allow all GET method from your specified domain to fetch assets

However, after I set CORS rule for my S3 bucket, the problem persists. It turns out that since I use Cloudfront as my assets CDN,  clients sent HTTP request to my Cloudfront server to fetch assets, but my Cloudfront server does NOT know I have allowed CORS request , so I need also set "Allowed Headers" for Cloudfront

- In Cloudfront service, click the distribution

![Edit Cloudfront Configuration][c_1]

- Under "Behaviors" tab, click "Edit"

![Edit Cloudfront Configuration 2][c_2]

- From "Forward Headers", choose "Whitelist", then add 3 headers to whitelist
  - Access-Control-Request-Headers
  - Access-Control-Request-Method
  - Origin

![Edit Cloudfront Configuration 3][c_3]

Now reload the page, the CORS error disappear, problem solved!

**Conclusion**

AWS is a powerful IAAS platform, with the flebility to fulfil most of the user scenarios. but this flexibility comes with a trade off: some of the features are not very well documented or even does not covered at all.

I have struggled with this problem for a couple of days, hopefully this post can save you some time if you encouter the same problem.

_Happy coding!_


<!-- images -->
[browser_error]: https://dl.dropboxusercontent.com/u/2390116/blog/images/cross_domain/chrome_error.png "browser block by CORS policy"
[s3_1]: https://dl.dropboxusercontent.com/u/2390116/blog/images/cross_domain/s3_1.png "S3 step 1"
[s3_2]: https://dl.dropboxusercontent.com/u/2390116/blog/images/cross_domain/s3_2.png "S3 step 2"
[c_1]: https://dl.dropboxusercontent.com/u/2390116/blog/images/cross_domain/cloudfront_1.png "Cloudfront step 1"
[c_2]: https://dl.dropboxusercontent.com/u/2390116/blog/images/cross_domain/cloudfront_2.png "Cloudfront step 2"
[c_3]: https://dl.dropboxusercontent.com/u/2390116/blog/images/cross_domain/cloudfront_3.png "Cloudfront step 3"

<!-- links -->
[1]: http://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html
