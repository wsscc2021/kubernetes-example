
If you use HPA(Horiozontal Pod Autoscaler), you must be install(deploy) the `Metrics-server`

And... cluster-autoscaler allow us automatic scale-up to AutoScalingGroup of aws.

metrics-server (*AWS Documents)
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/metrics-server.html

cluster-autoscaler (*AWS Documents)
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/cluster-autoscaler.html

You can create `service-account` using aws-cdk.
https://github.com/wsscc2021/aws-cdk-example/tree/master/services/eks