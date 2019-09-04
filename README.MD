# SQS Message Mover
SQS Mover lets you move messages from one AWS SQS queue to another. Useful when you need
to move deadletter queue messages back into the original queue.

## Features

* Reliable delivery. Messages are only deleted from the original queue if they 
were successfully un-queued to the destination.
* Messages are sent and received in batches for faster processing.
* Progress indicator.
* Queue name resolution. For ease of use, you only need to provide a queue name and not the full `arn` address. 

## Building

SQSMover can be built in the local directory with

```
go build -o sqsmover main.go
```

## Usage

```
sqsmover --help

usage: ./sqsmover --source=SOURCE --destination=DESTINATION [<flags>]

Flags:
      --help                     Show context-sensitive help (also try
                                 --help-long and --help-man).
  -s, --source=SOURCE            Source queue to move messages from
  -d, --destination=DESTINATION  Destination queue to move messages to
  -r, --region="eu-west-1"       AWS Region for source and destination queues
```

AWS credentials are automatically loaded from the ~/.aws/credentials file.

Examples:

Region will default to `us-west-2`, you can also override it with `--region` flag

```
./sqsmover --source=my_source_queue_name --destination=my_destination_queuename
./sqsmover --source=my_source_queue_name --destination=my_destination_queuename --region=eu-west-1

-- shorthand
./sqsmover -s my_source_queue_name -d my_destination_queuename -r eu-west-1
```



