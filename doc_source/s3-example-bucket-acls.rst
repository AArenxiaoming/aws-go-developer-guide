.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _s3-examples-bucket-acls:

#############################
Working with |S3| Bucket ACLs
#############################

.. meta::
   :description: Manage Amazon S3 bucket ACLs in using this AWS SDK for Go code example.
   :keywords: AWS SDK for Go code examples, S3, ACL, permissions

The following examples use |sdk-go| functions to:

* Get the access control lists (ACLs) on a bucket
* Get the ACLs on a bucket item
* Add a new user to the ACLs on a bucket
* Add a new user to the ACLs on a bucket item

You can download complete
versions of these example files from the
:doc-examples-go:`aws-doc-sdk-examples <s3>` repository on GitHub.

.. _s3-examples-bucket-acls-scenario:

Scenario
========

In these examples, a series of Go routines are used to manage ACLs
on your |S3| buckets.
The routines use the |sdk-go| to perform |S3| bucket operations using the
following methods of the |S3| client class:

* :sdk-go-api-deep:`GetBucketAcl <service/s3/#S3.GetBucketAcl>`
* :sdk-go-api-deep:`GetObjectAcl <service/s3/#S3.GetObjectAcl>`
* :sdk-go-api-deep:`PutBucketAcl <service/s3/#S3.PutBucketAcl>`
* :sdk-go-api-deep:`PutObjectAcl <service/s3/#S3.PutObjectAcl>`

.. _s3-examples-bucket-acls-prerequisites:

Prerequisites
=============

* You have :doc:`set up <setting-up>`, and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with |S3| bucket ACLs. To learn more, see :s3-dg:`Managing Access with ACLs <S3_ACLs_UsingACLs>` in the |S3-dg|.

.. _s3-examples-bucket-acls-get-bucket-acl:

Get a Bucket ACL
================

The
:sdk-go-api-deep:`GetBucketAcl <service/s3/#S3.GetBucketAcl>`
function gets the ACLs on a bucket.

The following example gets the ACLs on a bucket.

Create the file *GetBucketAcl.go*.
Add the following statements to import the Go and |sdk-go| packages used in the example.

.. literalinclude:: s3.go.get_bucket_acl.imports.txt
   :dedent: 0
   :language: go

Get the name of the bucket from the command line.

.. literalinclude:: s3.go.get_bucket_acl.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials
from the shared credentials file *~/.aws/credentials*,
the region from the shared configuration file *~/.aws/config*.

.. literalinclude:: s3.go.get_bucket_acl.session.txt
   :language: go
   :dedent: 4

Create a service client and call :sdk-go-api-deep:`GetBucketAcl <service/s3/#S3.GetBucketAcl>`,
passing in the name of the bucket.

.. literalinclude:: s3.go.get_bucket_acl.call.txt
   :language: go
   :dedent: 4

Loop through the results
and print out the name, type, and permission for the grantees.

.. literalinclude:: s3.go.get_bucket_acl.print.txt
   :language: go
   :dedent: 4

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/GetBucketAcl/GetBucketAcl.go>`_
on GitHub.

.. _s3-examples-bucket-acls-set-bucket-acl:

Set a Bucket ACL
================

The
:sdk-go-api-deep:`PutBucketAcl <service/s3/#S3.PutBucketAcl>`
function sets the ACLs on a bucket.

The following example gives a user with the specified email address READ access to a bucket.

Create the file *PutBucketAcl.go*.
Import the following Go and |sdk-go| packages used in the example.

.. literalinclude:: s3.go.put_bucket_acl.imports.txt
   :dedent: 0
   :language: go

Get the bucket name and user's email address from the command line.
If the optional permission parameter is supplied,
make sure it is one of the allowed values.

.. literalinclude:: s3.go.put_bucket_acl.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials
from the shared credentials file *~/.aws/credentials*,
the region from the shared configuration file *~/.aws/config*.

.. literalinclude:: s3.go.put_bucket_acl.session.txt
   :language: go
   :dedent: 4

Create a new service client and get the existing ACLs.

.. literalinclude:: s3.go.put_bucket_acl.service_acl.txt
   :language: go
   :dedent: 4
            
Append the new user to the list.

.. literalinclude:: s3.go.put_bucket_acl.add_grant.txt
   :language: go
   :dedent: 4

Call :sdk-go-api-deep:`PutBucketAcl <service/s3/#S3.PutBucketAcl>`,
passing in the parameter list.

.. literalinclude:: s3.go.put_bucket_acl.call.txt
   :language: go
   :dedent: 4

Display a messge indicating success.

.. literalinclude:: s3.go.put_bucket_acl.print.txt
   :language: go
   :dedent: 4

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/PutBucketAcl/PutBucketAcl.go>`_
on GitHub.

.. _s3-examples-bucket-acls-make-bucket-public-acl:

Making a Bucket Public using a Canned ACL
=========================================

As in the previous example, the
:sdk-go-api-deep:`PutBucketAcl <service/s3/#S3.PutBucketAcl>`
function sets the ACLs on a bucket.

The following example gives everyone read-only access to the items in the bucket.

Create the file *MakeBucketPublic.go*.
Add the following statements to import the Go and |sdk-go| packages used in the example.

.. literalinclude:: s3.go.make_bucket_public.imports.txt
   :dedent: 0
   :language: go

Get the bucket name from the command line.

.. literalinclude:: s3.go.make_bucket_public.args.txt
   :dedent: 4
   :language: go

Initialize the session that the SDK uses to load credentials
from the shared credentials file *~/.aws/credentials*
the region from the shared configuration file *~/.aws/config*.

.. literalinclude:: s3.go.make_bucket_public.session.txt
   :language: go
   :dedent: 4

Create a service client and the input for and call :sdk-go-api-deep:`PutBucketAcl <service/s3/#S3.PutBucketAcl>`.

.. literalinclude:: s3.go.make_bucket_public.call.txt
   :language: go
   :dedent: 4

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/MakeBucketPublic/MakeBucketPublic.go>`_
on GitHub.

.. _s3-examples-bucket-acls-get-bucket-object-acl:

Get a Bucket Object ACL
=======================

The
:sdk-go-api-deep:`PutObjectAcl <service/s3/#S3.PutObjectAcl>`
function sets the ACLs on a bucket item.

The following example gets the ACLs for a bucket item.

Create the file *GetObjectAcl.go*.
Add the following statements to import the Go and |sdk-go| packages used in the example.

.. literalinclude:: s3.go.get_object_acl.imports.txt
   :dedent: 0
   :language: go

Get the names of the bucket and object from the command line.

.. literalinclude:: s3.go.get_object_acl.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials
from the shared credentials file *~/.aws/credentials*,
the region from the shared configuration file *~/.aws/config*,
and create a new |S3| service client.

.. literalinclude:: s3.go.get_object_acl.session.txt
   :language: go
   :dedent: 4

Create a service client and call :sdk-go-api-deep:`GetObjectAcl <service/s3/#S3.GetObjectAcl>`,
passing in the names of the bucket and object.

.. literalinclude:: s3.go.get_object_acl.call.txt
   :language: go
   :dedent: 4

Loop through the results
and print out the name, type, and permission for the grantees.

.. literalinclude:: s3.go.get_object_acl.print.txt
   :language: go
   :dedent: 4

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/GetObjectAcl/GetObjectAcl.go>`_
on GitHub.

.. _s3-examples-bucket-acls-set-bucket-object-acl:

Set a Bucket Object ACL
=======================

The
:sdk-go-api-deep:`PutObjectAcl <service/s3/#S3.PutObjectAcl>`
function sets the ACLs on a bucket item.

The following example gives a user with the specified email address read access to a bucket item.

Create the file *PutObjectAcl.go*.
Add the following statements to import the Go and |sdk-go| packages used in the example.

.. literalinclude:: s3.go.put_object_acl.imports.txt
   :dedent: 0
   :language: go

Get the bucket name, object name, and user's email address from the command line.
If the optional permission parameter is supplied,
make sure it is one of the allowed values.

.. literalinclude:: s3.go.put_object_acl.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials
from the shared credentials file *~/.aws/credentials,
and create a service client.

.. literalinclude:: s3.go.put_object_acl.session.txt
   :language: go
   :dedent: 4

Call :sdk-go-api-deep:`PutObjectAcl <service/s3/#S3.PutObjectAcl>`,
passing in the bucket name, object name, and email address.

.. literalinclude:: s3.go.put_object_acl.call.txt
   :language: go
   :dedent: 4

Display a message indicating success.

.. literalinclude:: s3.go.put_object_acl.print.txt
   :language: go
   :dedent: 4

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/PutObjectAcl/PutObjectAcl.go>`_
on GitHub.
