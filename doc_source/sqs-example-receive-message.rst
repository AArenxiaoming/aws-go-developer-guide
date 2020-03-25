.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _examples-sqs-receive-message:

#######################################
Sending and Receiving Messages in |SQS|
#######################################

.. meta::
   :description: Send or receive a message from an Amazon SQS queue using this AWS SDK for Go code example.
   :keywords: AWS SDK for Go examples, SQS queues

These |sdk-go| examples show you how to:

* Send a message to an |SQS| queue
* Receive and delete a message from an |SQS| queue
* Send and receive messages from an |SQS| queue

You can download complete versions of these example files from the
:doc-examples-go:`aws-doc-sdk-examples <sqs>` repository on GitHub.

.. _sqs-receive-message-scenario:

The Scenario
============

These examples demonstrate sending, receiving, and deleting messages from an |SQS| queue.

The code uses these methods of the |SQS| client class:

* :sdk-go-api-deep:`SendMessage <service/sqs/#SQS.SendMessage>`
* :sdk-go-api-deep:`ReceiveMessage <service/sqs/#SQS.ReceiveMessage>`
* :sdk-go-api-deep:`DeleteMessage <service/sqs/#SQS.DeleteMessage>`
* :sdk-go-api-deep:`GetQueueUrl <service/sqs/#SQS.GetQueueUrl>`

.. _sqs-receive-message-prerequisites:

Prerequisites
=============

* You have :doc:`set up <setting-up>` and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with the details of |SQS| messages. To learn more, see
  :sqs-dg:`Sending a Message to an Amazon SQS Queue <sqs-send-message>` and
  :sqs-dg:`Receiving and Deleting a Message from an Amazon SQS Queue <sqs-receive-delete-message>`
  in the |SQS-dg|.


.. _sqs-example-send-message:

Send a Message to a Queue
=========================

Create a new Go file named :file:`SendMessage.go`.

You must import the relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.send_message.imports.txt
   :language: go

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.send_message.sess.txt
   :language: go
   :dedent: 4

Create a service client and send your message.
In this example, the message input passed to ``SendMessage``
represents information about a fiction best seller for a particular week and defines title,
author, and weeks on the list values.

.. literalinclude:: sqs.go.send_message.call.txt
   :language: go
   :dedent: 4

.. _sqs-example-receive-delete-message:

Receive and Delete a Message from a Queue
=========================================

Create a new Go file named :file:`DeleteMessage.go`.

You must import the relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.delete_message.imports.txt
   :language: go

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.delete_message.sess.txt
   :language: go
   :dedent: 4

Delete the message with the specified receipt handle from the queue.

.. literalinclude:: sqs.go.delete_message.call.txt
   :language: go
   :dedent: 4

