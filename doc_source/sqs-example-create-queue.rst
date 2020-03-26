.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _examples-sqs-using-queues:

##################
Using |SQS| Queues
##################

.. meta::
   :description: Learn to work with Amazon SQS queues using this AWS SDK for Go.
   :keywords: AWS SDK for Go code examples, SQS, create queue

These |sdk-go| examples show you how to:

*  List |SQS| queues
*  Create |SQS| queues
*  Get |SQS| queue URLs
*  Delete |SQS| queues

You can download complete versions of these example files from the
:doc-examples-go:`aws-doc-sdk-examples <sqs>` repository on GitHub.

.. _sqs-create-scenario:

Scenario
========

These examples demonstrate how to work with |SQS| queues.

The examples use the following methods of the |SQS| client class:

* :sdk-go-api-deep:`CreateQueue <service/sqs/#SQS.CreateQueue>`
* :sdk-go-api-deep:`DeleteQueue <service/sqs/#SQS.DeleteQueue>`
* :sdk-go-api-deep:`GetQueueUrl <service/sqs/#SQS.GetQueueUrl>`
* :sdk-go-api-deep:`ListQueues <service/sqs/#SQS.ListQueues>`

.. _sqs-create-prerequisites:

Prerequisites
=============

* You have :doc:`set up <setting-up>` and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with using |SQS|. To learn more, see :sqs-dg:`How Queues Work <sqs-how-it-works>` in the |SQS-dg|.

.. _sqs-example-list-queues:

List Queues
===========

Create a new Go file named :file:`ListQueues.go`. You must import the relevant Go and
|sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.list_queues.imports.txt
   :language: go


Initialize a session that the SDK will use to load credentials from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.list_queues.sess.txt
   :language: go
   :dedent: 4

Create a new service client and  call ``ListQueues``,
passing in ``nil`` to return all queues.

.. literalinclude:: sqs.go.list_queues.call.txt
   :language: go
   :dedent: 4

Display the list of queues.

.. literalinclude:: sqs.go.list_queues.display.txt
   :language: go
   :dedent: 4

Create a Queue
==============

Create a new Go file named :file:`CreateQueue.go`. You must import the relevant Go and
|sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.create_queue.imports.txt
   :language: go

Get the name of the queue from the command line.
If no name is supplied print an error message and quit.

.. literalinclude:: sqs.go.create_queue.args.txt
   :language: go
   :dedent: 4
            
Initialize a session that the SDK will use to load credentials from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.create_queue.sess.txt
   :language: go
   :dedent: 4

Create a service client and call ``CreateQueue`` with the name of the queue.

.. literalinclude:: sqs.go.create_queue.call.txt
   :language: go
   :dedent: 4

Print the URL of the queue.

.. literalinclude:: sqs.go.create_queue.print.txt
   :language: go
   :dedent: 4

Get a Queue URL
===============

Create a new Go file named :file:`GetQueueURL.go`. You must import the relevant Go and
|sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.get_queue_url.imports.txt
   :language: go

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.get_queue_url.sess.txt
   :language: go
   :dedent: 4

Create a service client and call ``GetQueueUrl`` passing in the queue name.

.. literalinclude:: sqs.go.get_queue_url.call.txt
   :language: go
   :dedent: 4

Print the URL of the queue.

.. literalinclude:: sqs.go.get_queue_url.print.txt
   :language: go
   :dedent: 4

Delete a Queue
==============

Create a new Go file named :file:`DeleteQueue.go`. You must import the relevant Go and
|sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.delete_queue.imports.txt
   :language: go

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.delete_queue.sess.txt
   :language: go
   :dedent: 4

Create a service client and call ``DeleteQueue`` passing in the queue name.

.. literalinclude:: sqs.go.delete_queue.call.txt
   :language: go
   :dedent: 4
