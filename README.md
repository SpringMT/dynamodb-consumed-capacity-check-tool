# dynamodb-consumed-capacity-check-tool

## How to use it
This tool requires an AWS credentials to access DynamoDB API. You need to configure an AWS credential where you required DynamoDB permissions. See details: https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html
```
sudo yum install golang git
git clone git@github.com:aws-samples/dynamodb-consumed-capacity-check-tool.git
cd ./dynamodb-consumed-capacity-check-tool
go build ./
./dynamodb-simple-benchmark -seqpk=true  -seqsk=true -table=benchmark -con=2 -max=10000 -datasize=100 -pk=US -sk=20200101120001 -region=ap-northeast-1 

```

option
```bash
  -con int
    	Concurrent Request No (default 2)
  -max int
    	max Request count (default 100)
  -pk string
    	partition key string (default "pk")
  -sk string
    	sort key string (default "sk")
  -datasize int
        test data attribute value datasize(random text)  (default 16byte)
  -region string
    	Use aws region (default "ap-northeast-1")
  -seqpk
    	bool:generate sequence pk data(ex:PK_1,PK_2...) or fix string
  -seqsk
    	bool:generate sequence sk data(ex:SK_1,SK_2...) or fix string

  -table string
    	Use DynamoDB table name (default "benchmark")

go run ./main.go -seqpk=true  -seqsk=true -table=benchmark_pro -con=2 -max=1 -pk=US -sk=20200101120001 -region=ap-northeast-1

###sample result

Init params true true
Set params tableName:benchmark concurrentNo:4 maxRequest:10 partitionKey:test sortKey:20200101120001 awsRegion:ap-northeast-1 generatePK:true generateSK:true
Start concurrency execute 2021-05-20 17:38:15.958701 +0900 JST m=+0.003459360
All test request:10,Concurrent:4,1thread count:2PUT benchmark test start
PUT start child execute : time:2021-05-20 17:38:15.959 +0900 JST m=+0.003759040,Counter:0,MaxRequets:10
PUT benchmark test start
PUT start child execute : time:2021-05-20 17:38:15.959625 +0900 JST m=+0.004383868,Counter:0,MaxRequets:10
PUT benchmark test start
PUT start child execute : time:2021-05-20 17:38:15.960374 +0900 JST m=+0.005133047,Counter:0,MaxRequets:10
PUT benchmark test start
PUT start child execute : time:2021-05-20 17:38:15.960777 +0900 JST m=+0.005536034,Counter:0,MaxRequets:10
PUT This goroutine  threadStartIndex: 6 threadCount: 2
PUT This goroutine  threadStartIndex: 2 threadCount: 2
PUT This goroutine  threadStartIndex: 0 threadCount: 2
PUT This goroutine  threadStartIndex: 4 threadCount: 2
PUT end child execute:time:2021-05-20 17:38:16.333561 +0900 JST m=+0.378317236,Counter:2,consumed capacity:2
GET benchmark test start
GET start child execute : time:2021-05-20 17:38:16.333601 +0900 JST m=+0.378358168,Counter:5,MaxRequets:10
GET This goroutine  threadStartIndex: 6 threadCount: 2
PUT end child execute:time:2021-05-20 17:38:16.340118 +0900 JST m=+0.384874727,Counter:2,consumed capacity:2
GET benchmark test start
GET start child execute : time:2021-05-20 17:38:16.340173 +0900 JST m=+0.384929213,Counter:6,MaxRequets:10
PUT end child execute:time:2021-05-20 17:38:16.340404 +0900 JST m=+0.385160302,Counter:2,consumed capacity:2
GET benchmark test start
GET start child execute : time:2021-05-20 17:38:16.340428 +0900 JST m=+0.385184301,Counter:7,MaxRequets:10
GET This goroutine  threadStartIndex: 0 threadCount: 2
GET This goroutine  threadStartIndex: 2 threadCount: 2
PUT end child execute:time:2021-05-20 17:38:16.342528 +0900 JST m=+0.387284448,Counter:2,consumed capacity:2
GET benchmark test start
GET start child execute : time:2021-05-20 17:38:16.342576 +0900 JST m=+0.387332826,Counter:8,MaxRequets:10
GET This goroutine  threadStartIndex: 4 threadCount: 2
GET end child execute:time:2021-05-20 17:38:16.373252 +0900 JST m=+0.418007996,Counter:2,consumed capacity:1
GET end child execute:time:2021-05-20 17:38:16.379856 +0900 JST m=+0.424612872,Counter:2,consumed capacity:1
GET end child execute:time:2021-05-20 17:38:16.380686 +0900 JST m=+0.425442437,Counter:2,consumed capacity:1
GET end child execute:time:2021-05-20 17:38:16.384071 +0900 JST m=+0.428827415,Counter:2,consumed capacity:1
End all execute.
Benchmark start time:2021-05-20 17:38:15.958701 +0900 JST m=+0.003459360
Benchmark end time:2021-05-20 17:38:16.384138 +0900 JST m=+0.428894146
All request count:16,success:16,error0
Benchmark total time:0.425434786sec
Avg throughput:37.60858426842416req/sec
Benchmark total consumend capacity
PUT:8
GET:4 (RoundDown)
Set params tableName:benchmark concurrentNo:4 maxRequest:10 partitionKey:test sortKey:20200101120001 awsRegion:ap-northeast-1 generatePK:true generateSK:true

Process finished with exit code 0


```
This tool is intended for testing simple workload. With this tool, you can achieve followings:

* Concurrency control
* Simple generation of PartitionKey and SortKey strings
* Set the number of requests

I created this primarily to confirm the mechanism.
https://aws.amazon.com/jp/about-aws/whats-new/2019/11/amazon-dynamodb-adaptive-capacity-now-handles-imbalanced-workloads-better-by-isolating-frequently-accessed-items-automatically/


## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

# License
This library is licensed under the MIT-0 License. See the LICENSE file.
