.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _examples-s3-website:

#########################################
Using an |S3| Bucket as a Static Web Host
#########################################

.. meta::
   :description: Set up an Amazon S3 bucket as a static web host using this AWS SDK for Go code example.
   :keywords: AWS SDK for Go code examples, S3 static web host


This |sdk-go| example shows you how to configure an |S3| bucket to act as a static web host. You can download
complete versions of these example files from the :doc-examples-go:`aws-doc-sdk-examples <s3>` repository on GitHub.

.. _s3-website-scenario:

Scenario
========

In this example, you use a series of Go routines to configure any of your
buckets to act as a static web host. The routines use the |sdk-go| to configure a selected |S3|
bucket using these methods of the |S3| client class:

* GetBucketWebsite
* PutBucketWebsite
* DeleteBucketWebsite

For more information about using an |S3| bucket as a static web host, see
:s3-dg:`Hosting a Static Website on Amazon S3 <WebsiteHosting>` in the |S3-dg|.

.. _s3-website-prerequisites:

Prerequisites
=============

* You have :doc:`set up <setting-up>`, and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with hosting static websites on |S3|. To learn more,
  see :s3-dg:`Hosting a Static Website on Amazon S3 <WebsiteHosting>` in the |S3-dg|.

.. _s3-example-retrieve-config:

Retrieve a Bucket's Website Configuration
=========================================

Create a new Go file named :file:`GetBucketWebsite.go`.
Import the relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: s3.go.get_bucket_website.imports.txt
   :language: go
   :dedent: 0

Get the name of the bucket from the command line.

.. literalinclude:: s3.go.get_bucket_website.args.txt
   :language: go
   :dedent: 4

Initialize a session that the SDK will use to load credentials from the shared credentials file,
~/.aws/credentials, and create a new S3 service client.

.. literalinclude:: s3.go.get_bucket_website.session.txt
   :language: go
   :dedent: 4

Create a service object and call :sdk-go-api-deep:`GetBucketWebsite <service/s3/#S3.GetBucketWebsite>`
to get the bucket configuration.

.. literalinclude:: s3.go.get_bucket_website.call.txt
   :language: go
   :dedent: 4

If :code:`GetBucketWebsite` returns an error, print an error message and return.
Check the error for the ``NoSuchWebsiteConfiguration`` error code, which tells you that the bucket doesn't
have a website configured.

.. literalinclude:: s3.go.get_bucket_website.error.txt
   :language: go
   :dedent: 4

Print the bucket's website configuration.

.. literalinclude:: s3.go.get_bucket_website.print.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/GetBucketWebsite/GetBucketWebsite.go>`_
on GitHub.

.. _s3-example-set-bucket-website:

Set a Bucket's Website Configuration
====================================

The |S3|
:sdk-go-api-deep:`PutBucketWebsite <service/s3/#S3.PutBucketWebsite>` operation
sets the website configuration on a bucket, replacing any existing configuration.

Create a new Go file named :file:`SetBucketWebsite.go`.
Import the relevant Go and
|sdk-go| packages by adding the following lines.

.. literalinclude:: s3.go.put_bucket_website.imports.txt
   :language: go
   :dedent: 0

Get the names of the bucket, index page, and optional error page from the command line.

.. literalinclude:: s3.go.put_bucket_website.args.txt
   :language: go
   :dedent: 4

Initialize a session that the SDK will use to load configuration, credentials,
and region information from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: s3.go.put_bucket_website.session.txt
   :language: go
   :dedent: 4

Create a service client,
and call :sdk-go-api-deep:`PutBucketWebsite <service/s3/#S3.PutBucketWebsite>`,
including the bucket name and index document details.
If the user passed in an error page, add that to the parameters.

.. literalinclude:: s3.go.put_bucket_website.call.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/SetBucketWebsite/SetBucketWebsite.go>`_
on GitHub.

.. _s3-example-delete-website:

Delete Website Configuration on a Bucket
========================================

Create a Go file named :file:`DeleteBucketWebsite.go`.
Import the relevant Go and |sdk-go| packages.

.. literalinclude:: s3.go.delete_bucket_website.imports
   :dedent: 0
   :language: go

Get the name of the bucket for which you want to delete the
website configuration from the command line.

.. literalinclude:: s3.go.delete_bucket_website.args.txt
   :language: go
   :dedent: 4

Initialize a session that the SDK will use to load
configuration, credentials, and region information from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: s3.go.delete_bucket_website.session.txt
   :language: go
   :dedent: 4

Create a service client and call ``DeleteBucketWebsite``,
passing in the name of the bucket.

.. literalinclude:: s3.go.delete_bucket_website.call.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/DeleteBucketWebsite/DeleteBucketWebsite.go>`_
on GitHub.
