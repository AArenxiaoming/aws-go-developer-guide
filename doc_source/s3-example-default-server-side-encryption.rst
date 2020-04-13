.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _aws-go-sdk-s3-example-default-server-side-encryption:

##############################################################
Setting Default Server-Side Encryption for an Amazon S3 Bucket
##############################################################

.. meta::
    :description:
        Encrypt Amazon S3 bucket objects by default using this AWS SDK for Go code example.
    :keywords: AWS SDK for Go code examples

The following example uses the
:sdk-go-api-deep:`PutBucketEncryption <service/s3/#S3.PutBucketEncryption>`
method to enable KMS server-side encryption on any objects added to
:code:`myBucket`.

The only exception is if the user configures their request to explicitly
use server-side encryption. In that case, the specified encryption takes precedence.

Choose :code:`Copy` to save the code locally.

Create the file *SetDefaultEncryption.go*.

Import the required packages.

.. literalinclude:: s3.go.set_default_encryption.imports.txt
   :dedent: 0
   :language: go

Get the bucket name and KMS key from the command line.
You can create a KMS key using the :doc:`kms-example-create-key` example.

.. literalinclude:: s3.go.set_default_encryption.args.txt
   :dedent: 4
   :language: go

Create a session.

.. literalinclude:: s3.go.set_default_encryption.session
   :dedent: 4
   :language: go

Create a service client and call :code:`PutBucketEncryption`.

.. literalinclude:: s3.go.set_default_encryption.call.txt
   :dedent: 4
   :language: go

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/SetDefaultEncryption/SetDefaultEncryption.go>`_
on GitHub.
