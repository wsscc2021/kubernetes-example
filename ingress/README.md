
## aws-load-balancer-controller

ingress 리소스를 생성하기 위해서는 aws-load-balancer-controller를 먼저 생성해야 합니다.

REF: https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/deploy/installation/

1. IAM - OIDC Provider 생성

    ```
    eksctl utils associate-iam-oidc-provider \
        --region <region-code> \
        --cluster <your-cluster-name> \
        --approve
    ```

2. IAM - Policy 생성

    ```powershell
    curl -o iam-policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.1/docs/install/iam_policy.json
    ```
    ```powershell
    aws iam create-policy \
        --policy-name AWSLoadBalancerControllerIAMPolicy \
        --policy-document file://iam-policy.json
    ```

3. IAM - Role 생성

    ```powershell
    eksctl create iamserviceaccount \
        --cluster=<cluster-name> \
        --namespace=kube-system \
        --name=aws-load-balancer-controller \
        --attach-policy-arn=arn:aws:iam::<AWS_ACCOUNT_ID>:policy/AWSLoadBalancerControllerIAMPolicy \
        --override-existing-serviceaccounts \
        --region <region-code> \
        --approve
    ```

4. TargetGroupBinding CRDs 생성

    ```powershell
    kubectl apply -k "github.com/aws/eks-charts/stable/aws-load-balancer-controller//crds?ref=master"
    ```

5. Helm - Repo 추가

    ```powershell
    helm repo add eks https://aws.github.io/eks-charts
    ```

6. Helm - Install from chart

    ```powershell
    helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
        -n kube-system \
        --set clusterName=<cluster-name> \
        --set serviceAccount.create=false \
        --set serviceAccount.name=aws-load-balancer-controller
    ```

    - if you have tolerations options
    
        ```
        helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
            -n kube-system \
            --set clusterName=<cluster-name> \
            --set serviceAccount.create=false \
            --set serviceAccount.name=aws-load-balancer-controller \
            --set tolerations[0].key="key01" \
            --set tolerations[0].value="value01" \
            --set tolerations[0].effect="NoSchedule"
        ```

7. Subnet Tag 추가

    Subnet Discovery를 위해 Subnet에 태그를 추가합니다.

    - public & private subnets

        `kubernetes.io/cluster/${cluster-name}`: `owned` or `shared`

    - public subnets

        `kubernetes.io/role/elb` : `1`

    - private subnets

        `kubernetes.io/role/internal-elb` : `1`



Github Source
https://github.com/kubernetes-sigs/aws-load-balancer-controller

Guide Page
https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/

You can create service-account using aws-cdk.
https://github.com/wsscc2021/aws-cdk-example/tree/master/services/eks