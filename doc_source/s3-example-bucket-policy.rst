.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _examples-s3-bucket-policies:

#################################
Working with |S3| Bucket Policies
#################################

.. meta::
   :description: Work with Amazon S3 bucket policies using this AWS SDK for Go code example.
   :keywords: AWS SDK for Go examples, S3, policy, ACL, permissions

This |sdk-go| example shows you how to retrieve, display, and set |S3| bucket polices. You can download
complete versions of these example files from the
:doc-examples-go:`aws-doc-sdk-examples <s3>` repository on GitHub.

.. _s3-bucket-policies-scenario:

Scenario
========

In this example, you use a series of Go routines to retrieve or set a bucket policy on an
|S3| bucket. The routines use the |sdk-go| to configure policy for a selected |S3| bucket using
these methods of the |S3| client class:

* :sdk-go-api-deep:`GetBucketPolicy <service/s3/#S3.GetBucketPolicy>`
* :sdk-go-api-deep:`PutBucketPolicy <service/s3/#S3.PutBucketPolicy>`
* :sdk-go-api-deep:`DeleteBucketPolicy <service/s3/#S3.DeleteBucketPolicy>`

For more information about bucket policies for |S3| buckets, see
:s3-dg:`Using Bucket Policies and User Policies <using-iam-policies>` in the |S3-dg|.

.. _s3-bucket-policies-prerequisites:

Prerequisites
=============

* You have  :doc:`set up <setting-up>`, and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with |S3| bucket polices. To learn more, see :s3-dg:`Using Bucket Policies and User Policies <using-iam-policies>` in the |S3-dg|.

.. _s3-example-get-policy:

Retrieve and Display a Bucket Policy
====================================

Create a new Go file named :file:`GetBucketPolicy.go`. You must import the relevant
Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: s3.go.get_bucket_policy.imports.txt
   :dedent: 0
   :language: go

Get the bucket name from the command line.

.. literalinclude:: s3.go.get_bucket_policy.args.txt
   :language: go
   :dedent: 4

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials, and create a new S3 service client.

.. literalinclude:: s3.go.get_bucket_policy.session.txt
   :language: go
   :dedent: 4

Create a service object and call :sdk-go-api-deep:`GetBucketPolicy <service/s3/#S3.GetBucketPolicy>`
to fetch the policy.

.. literalinclude:: s3.go.get_bucket_policy.call.txt
   :language: go
   :dedent: 4

Use Go's JSON package to get a string version of the Policy.

.. literalinclude:: s3.go.get_bucket_policy.string.txt
   :language: go
   :dedent: 4

Display the policy.

.. literalinclude:: s3.go.get_bucket_policy.print.txt
   :language: go
   :dedent: 4

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/GetBucketPolicy/GetBucketPolicy.go>`_
on GitHub.
            
.. _s3-example-set-policy:

Set Bucket Policy
=================

This routine sets the policy for a bucket. If the bucket doesn't exist, or there was
an error, an error message will be printed instead.

Import the relevant packages.

.. literalinclude:: s3.go.set_bucket_policy.imports.txt
   :dedent: 0
   :language: go

Get the name of the bucket from the command line.

.. literalinclude:: s3.go.set_bucket_policy.args.txt
   :dedent: 0
   :language: go
              
Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials

.. literalinclude:: s3.go.set_bucket_policy.session.txt
   :lines: 17-26
   :language: go

Create a service object and a policy, filling in the bucket as the resource.
Use the JSON package to marshal the policy into a JSON value,
and call :sdk-go-api-deep:`PutBucketPolicy <service/s3/#S3.PutBucketPolicy>`
to add the policy to the bucket.

.. literalinclude:: s3.go.set_bucket_policy.call.txt
   :dedent: 4
   :language: go

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/SetBucketPolicy/SetBucketPolicy.go>`_
on GitHub.
