.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _aws-go-sdk-s3-example-server-side-encryption-with-kms:

#################################################################
Encrypting an Amazon S3 Bucket Object on the Server Using AWS KMS
#################################################################

.. meta::
    :description:
        Encrypt Amazon S3 bucket objects on the server with AWS KMS using this AWS SDK for Go code example.
    :keywords: AWS SDK for Go code examples

The following example uses the
:sdk-go-api-deep:`PutObject <service/s3/#S3.PutObject>`
method to add the object :code:`myItem` to the bucket
:code:`myBucket` with server-side encryption set to AWS KMS.

Note that this differs from :doc:`s3-example-default-server-side-encryption`,
is in that case, the objects are encrypted without you having to explicitly perform the operation.

Choose :code:`Copy` to save the code locally.

Create the file *EncryptOnServerWithKms.go*.

Add the required packages.

.. literalinclude:: s3.go.encrypt_on_server_with_kms.imports.txt
   :dedent: 0
   :language: go

Get the bucket name, object name, and KMS key ID from the command line
You can create a KMS key using the :doc:`kms-example-create-key` example.

.. literalinclude:: s3.go.encrypt_on_server_with_kms.args.txt
   :dedent: 4
   :language: go

Create a session object.

.. literalinclude:: s3.go.encrypt_on_server_with_kms.session.txt
   :dedent: 4
   :language: go

Create a service object and call :code:`put_object`.
Notice that the :code:`server_side_encryption` property is set to :code:`aws:kms`,
indicating that |S3| encrypts the object using AWS KMS.

.. literalinclude:: s3.go.encrypt_on_server_with_kms.call.txt
   :dedent: 4
   :language: go

See the `complete example
<https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/go/s3/EncryptOnServerWithKms/EncryptOnServerWithKms.go>`_
on GitHub.
