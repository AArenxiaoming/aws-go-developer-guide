.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _s3-examples-bucket-ops:

#######################################
Performing Basic |S3| Bucket Operations
#######################################

.. meta::
   :description: Create and use Amazon S3 buckets using this AWS SDK for Go code example.
   :keywords: AWS SDK for Go code examples, S3, list buckets, create bucket,
              list bucket items, add file to bucket, download file from
              bucket, copy bucket item to another bucket, delete bucket
              item, delete all bucket items, restore bucket item,
              delete bucket

These |sdk-go| examples show you how to perform the following operations on |S3| buckets and bucket
items:

* List the buckets in your account
* Create a bucket
* List the items in a bucket
* Upload a file to a bucket
* Download a bucket item
* Copy a bucket item to another bucket
* Delete a bucket item
* Delete all the items in a bucket
* Restore a bucket item
* Delete a bucket
* List the users with administrator privileges

You can download complete versions of these example files from the
:doc-examples-go:`aws-doc-sdk-examples <s3>` repository on GitHub.

.. _s3-examples-bucket-ops-scenario:

Scenario
========

In these examples, a series of Go routines are used to perform operations on your |S3| buckets. The
routines use the |sdk-go| to perform |S3| bucket operations using the following methods of the |S3|
client class, unless otherwise noted:

* :sdk-go-api-deep:`ListBuckets <service/s3/#S3.ListBuckets>`
* :sdk-go-api-deep:`CreateBucket <service/s3/#S3.CreateBucket>`
* :sdk-go-api-deep:`ListObjects <service/s3/#S3.ListObjects>`
* :sdk-go-api-deep:`Upload <service/s3/s3manager/#Uploader.Upload>` (from the
  **s3manager.NewUploader** class)
* :sdk-go-api-deep:`Download <service/s3/s3manager/#Downloader.Download>` (from the
  **s3manager.NewDownloader** class)
* :sdk-go-api-deep:`CopyObject <service/s3/#S3.CopyObject>`
* :sdk-go-api-deep:`DeleteObject <service/s3/#S3.DeleteObject>`
* :sdk-go-api-deep:`DeleteObjects <service/s3/#S3.DeleteObjects>`
* :sdk-go-api-deep:`RestoreObject <service/s3/#S3.RestoreObject>`
* :sdk-go-api-deep:`DeleteBucket <service/s3/#S3.DeleteBucket>`

.. _s3-examples-bucket-ops-prerequisites:

Prerequisites
=============

* You have :doc:`set up <setting-up>` and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with buckets. To learn more, see
  :S3-dg:`Working with Amazon S3 Buckets <UsingBucket>` in the |S3-dg|.

.. _s3-examples-bucket-ops-list-buckets:

List Buckets
============

The :sdk-go-api-deep:`ListBuckets <service/s3/#S3.ListBuckets>` function lists the buckets in your
account.

The following example lists the buckets in your account. There are no command line arguments.

.. note::
   This example might not display all of your buckets.
   See the  
   :ref:`pagination <using-pagination-methods>`
   section for details.

Create the file *ListBuckets.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.list_buckets.imports.txt
   :language: go

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials.

.. literalinclude:: s3.go.list_buckets.imports.session.txt
   :language: go
   :dedent: 4

Create a service client and call :sdk-go-api-deep:`ListBuckets <service/s3/#S3.ListBuckets>`.
Pass ``nil`` as no filters are applied to the returned list.

.. literalinclude:: s3.go.list_buckets.imports.call.txt
   :language: go
   :dedent: 4

Loop
through the buckets, printing the name and creation date of each bucket.

.. literalinclude:: s3.go.list_buckets.imports.print.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/ListBuckets/ListBuckets.go>`_
on GitHub.

.. _s3-examples-bucket-ops-create-bucket:

Create a Bucket
===============

The :sdk-go-api-deep:`CreateBucket <service/s3/#S3.CreateBucket>` function creates a bucket in your
account.

The following example creates a bucket with the name specified as a command line argument. You must
specify a globally unique name for the bucket.

Create the file *CreateBucket.go*. Import the following Go and |sdk-go| packages.

.. literalinclude:: s3.go.create_bucket.imports.txt
   :dedent: 0
   :language: go

The program requires one argument, the name of the bucket to create.

.. literalinclude:: s3.go.create_bucket.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials, and create a new S3 service client.

.. literalinclude:: s3.go.create_bucket.imports.session.txt
   :language: go
   :dedent: 4

Create a service client and all :sdk-go-api-deep:`CreateBucket <service/s3/#S3.CreateBucket>`,
passing in the bucket name.

.. literalinclude:: s3.go.create_bucket.call.txt
   :language: go
   :dedent: 4

Wait for a for the bucket to be created.

.. literalinclude:: s3.go.create_bucket.wait.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/CreateBucket/CreateBucket.go>`_
on GitHub.

.. _s3-examples-bucket-ops-list-bucket-items:

List Bucket Items
=================

The :sdk-go-api-deep:`ListObjects <service/s3/#S3.ListObjectsV2>` function lists the items in a bucket.

The following example lists the items in the bucket with the name specified as a command line
argument.

.. note::
   This example might not display all of your objects.
   See the  
   :ref:`pagination <using-pagination-methods>`
   section for details.

Create the file *ListObjects.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.list_objects.imports.txt
   :dedent: 0
   :language: go

The program requires one command line argument, the name of the bucket.

.. literalinclude:: s3.go.list_objects.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials.

.. literalinclude:: s3.go.list_objects.session.txt
   :language: go
   :dedent: 4

Create a service client and call :sdk-go-api-deep:`ListObjects <service/s3/#S3.ListObjectsV2>`,
passing in the name of the bucket.

.. literalinclude:: s3.go.list_objects.call.txt
   :language: go
   :dedent: 4

Loop through the items, printing the
name, last modified date, size, and storage class of each item.

.. literalinclude:: s3.go.list_objects.print.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/ListObjects/ListObjects.go>`_
on GitHub.

.. _s3-examples-bucket-ops-upload-file-to-bucket:

Upload a File to a Bucket
=========================

The :sdk-go-api-deep:`Upload <service/s3/s3manager/#Uploader.Upload>` function uploads an object to
a bucket.

The following example uploads a file to a bucket with the names specified as command line arguments.

Create the file *UploadObject.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.upload_object.imports.txt
   :dedent: 0
   :language: go

Get the bucket and file name from the command line arguments

.. literalinclude:: s3.go.upload_object.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials, and create a ``NewUploader`` object.

.. literalinclude:: s3.go.upload_object.session.txt
   :language: go
   :dedent: 4

Open the file.

.. literalinclude:: s3.go.upload_object.open.txt
   :language: go
   :dedent: 4


Upload the file to the bucket.

.. literalinclude:: s3.go.upload_object.call.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/UploadObject/UploadObject.go>`_
on GitHub.

.. _s3-examples-bucket-ops-download-file-from-bucket:

Download a File from a Bucket
=============================

The :sdk-go-api-deep:`Download <service/s3/s3manager/#Downloader.Download>` function downloads an
object from a bucket.

The following example downloads an item from a bucket with the names specified as command line
arguments.

Create the file *DownloadObject.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.download_object.imports.txt
   :dedent: 0
   :language: go

Get the bucket and file name from the command line arguments.

.. literalinclude:: s3.go.download_object.args.txt
   :language: go
   :dedent: 4

Create a session that loads credentials from the shared
credentials file *~/.aws/credentials.

.. literalinclude:: s3.go.download_object.session.txt
   :language: go
   :dedent: 4

Create the file.

.. literalinclude:: s3.go.download_object.create.txt
   :language: go
   :dedent: 4

Create a ``NewDownloader`` object and download the file.

.. literalinclude:: s3.go.download_object.call.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/Downloadobject/Downloadobject.go>`_
on GitHub.

.. _s3-examples-bucket-ops-copy-bucket-item:

Copy an Item from one Bucket to Another
=======================================

The :sdk-go-api-deep:`CopyObject <service/s3/#S3.CopyObject>` function copies an object from one
bucket to another.

The following example copies an item from one bucket to another with the names specified as command
line arguments.

Create the file *CopyObject.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.copy_object.imports.txt
   :dedent: 0
   :language: go

Get the names of the bucket containing the item, the item to copy, and the name of the bucket to
which the item is copied.

.. literalinclude:: s3.go.copy_object.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials, and create a new |S3| service client.

.. literalinclude:: s3.go.copy_object.session.txt
   :language: go
   :dedent: 4

Create a service client and call :sdk-go-api-deep:`CopyObject <service/s3/#S3.CopyObject>`,
with the names of the bucket containing the item, the item to copy,
and the name of the bucket to which the item is copied.

.. literalinclude:: s3.go.copy_object.call.txt
   :language: go
   :dedent: 4

Wait for the item to be copied.

.. literalinclude:: s3.go.copy_object.wait.txt
   :language: go
   :dedent: 4

Notify the user that the copy succeeded.

.. literalinclude:: s3.go.copy_object.print.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/CopyObject/CopyObject.go>`_
on GitHub.

.. _s3-examples-bucket-ops-delete-bucket-item:

Delete an Item in a Bucket
==========================

The :sdk-go-api-deep:`DeleteObject <service/s3/#S3.DeleteObject>` function deletes an object from a
bucket.

The following example deletes an item from a bucket with the names specified as command line
arguments.

Create the file *DeleteObject.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.delete_object.imports.txt
   :language: go
   :dedent: 0

Get the name of the bucket and object to delete.

.. literalinclude:: s3.go.delete_object.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials.

.. literalinclude:: s3.go.delete_object.session.txt
   :language: go
   :dedent: 4

Create a service object and call :sdk-go-api-deep:`DeleteObject <service/s3/#S3.DeleteObject>`,
passing in the names of the bucket and object to delete.

.. literalinclude:: s3.go.delete_object.call.txt
   :language: go
   :dedent: 4

Wait until the object no longer exists.

.. literalinclude:: s3.go.delete_object.wait.txt
   :language: go
   :dedent: 4

Print a message.

.. literalinclude:: s3.go.delete_object.print.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/DeleteObject/DeleteObject.go>`_
on GitHub.

.. _s3-examples-bucket-ops-delete-all-bucket-items:

Delete All the Items in a Bucket
================================

The :sdk-go-api-deep:`DeleteObjects <service/s3/#S3.DeleteObjects>` function deletes objects from a
bucket.

The following example deletes all the items from a bucket with the bucket name specified as a
command line argument.

Create the file *DeleteObjects.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.delete_objects.imports.txt
   :language: go
   :dedent: 0

Get the name of the bucket.

.. literalinclude:: s3.go.delete_objects.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials.

.. literalinclude:: s3.go.delete_objects.session.txt
   :language: go
   :dedent: 4

Create a client object, a list iterator to iterate through the list of bucket objects,
and call `NewBatchDeleteWithClient` to delete the object.

.. literalinclude:: s3.go.delete_objects.call.txt
   :language: go
   :dedent: 4

Inform the user that the objects were deleted.

.. literalinclude:: s3.go.delete_objects.print
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/DeleteObjects/DeleteObjects.go>`_
on GitHub.

.. _s3-examples-bucket-ops-restore-bucket-item:

Restore a Bucket Item
=====================

The :sdk-go-api-deep:`RestoreObject <service/s3/#S3.RestoreObject>` function restores an item in a
bucket.

The following example restores an item to a bucket.

Create the file *RestoreObject.go*. Add the following statements to import the Go and |sdk-go|
packages used in the example.

.. literalinclude:: s3.go.restore_object.imports.txt
   :lines: go
   :dedent: 0

The program requires two arguments, the names of the bucket and object to restore.

.. literalinclude:: s3.go.restore_object.args
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials.

.. literalinclude:: s3.go.restore_object.session.txt
   :language: go
   :dedent: 4

Create a service object and call :sdk-go-api-deep:`RestoreObject <service/s3/#S3.RestoreObject>`,
passing in the bucket and object names and the number of days to temporarily restore.

.. literalinclude:: s3.go.restore_object.call.txt
   :language: go
   :dedent: 4

Inform the user that the bucket should be restored.

.. literalinclude:: s3.go.restore_object.print.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/RestoreObject/RestoreObject.go>`_
on GitHub.

.. _s3-examples-bucket-ops-delete-bucket:

Delete a Bucket
===============

The :sdk-go-api-deep:`DeleteBucket <service/s3/#S3.DeleteBucket>` function deletes a bucket.

The following example deletes the bucket with the name specified as a command line argument.

Create the file *DeleteBucket.go*. Import the following Go and |sdk-go| packages.

.. literalinclude:: 
   :language: go
   :dedent: 0

The program requires one argument, the name of the bucket to delete.

.. literalinclude:: s3.go.delete_bucket.args.txt
   :language: go
   :dedent: 4

Initialize the session that the SDK uses to load credentials from the shared credentials file
*~/.aws/credentials, and create a new S3 service client.

.. literalinclude:: s3.go.delete_bucket.imports.session.txt
   :language: go
   :dedent: 4

Create a service client and call :sdk-go-api-deep:`DeleteBucket <service/s3/#S3.DeleteBucket>`,
passing in the bucket name.

.. literalinclude:: s3.go.delete_bucket.call.txt
   :language: go
   :dedent: 4

Wait for a notification that the bucket was deleted. 

.. literalinclude:: s3.go.delete_bucket.wait.txt
   :language: go
   :dedent: 4

See the
`complete example <https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/DeleteBucket/DeleteBucket.go>`_
on GitHub.
