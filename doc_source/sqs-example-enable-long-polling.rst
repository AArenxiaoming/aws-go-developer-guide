.. Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _examples-sqs-long-polling:

#####################################
Enabling Long Polling in |SQS| Queues
#####################################

.. meta::
   :description: Enable long polling with Amazon SQS queues using this AWS SDK code example.
   :keywords: AWS SDK for Go code examples, SQS, create queue


These |sdk-go| examples show you how to:

* Enable long polling when you create an |SQS| queue
* Enable long polling on an existing |SQS| queue
* Enable long polling when a message is received

You can download complete versions of these example files from the
:doc-examples-go:`aws-doc-sdk-examples <sqs>` repository on GitHub.

.. _sqs-long-polling-scenario:

Scenario
========

Long polling reduces the number of empty responses by allowing |SQS|
to wait a specified time for a message to become available in the queue before sending a response.
Also, long polling eliminates false empty responses by querying all of the servers instead of a
sampling of servers. To enable long polling, you must specify a non-zero wait time for received
messages. You can do this by setting the ``ReceiveMessageWaitTimeSeconds`` parameter of a queue
or by
setting the ``WaitTimeSeconds`` parameter on a message when it is received.

The code uses these methods of the |SQS| client class:

* :sdk-go-api-deep:`SetQueueAttributes <service/sqs/#SQS.SetQueueAttributes>`
* :sdk-go-api-deep:`ReceiveMessage <service/sqs/#SQS.ReceiveMessage>`
* :sdk-go-api-deep:`CreateQueue <service/sqs/#SQS.CreateQueue>`

.. _sqs-long-polling-prerequisites:

Prerequisites
=============

* You have :doc:`set up <setting-up>` and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with |SQS| polling. To learn more, see
  :sqs-dg:`Long Polling <sqs-long-polling>` in the |SQS-dg|.


.. _sqs-example-create-queue-long-pollling:

Enable Long Polling When Creating a Queue
=========================================

This example creates a queue with long polling enabled. If the queue already exists,
no error is returned.

Create a new Go file named :file:`CreateLPQueue.go`. You must import the
relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.create_lp_queue.imports.txt
   :language: go

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.create_lp_queue.sess.txt
   :language: go
   :dedent: 4

Create the queue with long polling enabled. Print any errors or a success message.

.. literalinclude:: sqs.go.create_lp_queue.call.txt
   :language: go
   :dedent: 4

Enable Long Polling on an Existing Queue
========================================

Create a new Go file named :file:`ConfigureLPQueue.go`.

You must import the relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.configure_lp_queue.imports.txt
   :language: go

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.configure_lp_queue.sess.txt
   :language: go

Update the queue with the URL `queueURL` to enable long polling
with a call to ``SetQueueAttributes``, passing in the
queue URL. Print any errors or a success message.

.. literalinclude:: sqs.go.configure_lp_queue.set_attributes.txt
   :language: go
   :dedent: 4

Enable Long Polling on Message Receipt
======================================

Create a new Go file named :file:`ReceiveLPMessage.go`.

You must import the relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: sqs.go.receive_lp_message.imports.txt
   :language: go

This example takes three flags, the -u flag is the queue URL, the -v flag contains the
visibility value, and the -w flag contains the wait time value.

.. literalinclude:: sqs.go.receive_lp_message.args.txt
   :language: go
   :dedent: 4

Initialize a session that the SDK will use to load credentials
from the shared credentials file, ~/.aws/credentials.

.. literalinclude:: sqs.go.receive_lp_message.sess.txt
   :language: go
   :dedent: 4

Create a service client and receive a message from the queue with long polling enabled with a call to
``ReceiveMessage``, passing in the queue URL.

.. literalinclude:: sqs.go.receive_lp_message.call.txt
   :language: go
   :dedent: 4
