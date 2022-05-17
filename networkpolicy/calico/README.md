
refer
- https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/calico.html
- https://kubernetes.io/ko/docs/concepts/services-networking/network-policies/


## install calico plugin

1. add helm repo

    ```powershell
    helm repo add projectcalico https://docs.projectcalico.org/charts
    ```

2. update helm repo

    ```powershell
    helm repo update
    ```

3. create namespace

    ```powershell
    kubectl create namespace calico-system
    ```

4. write `values.yaml`

    ```powershell
    installation:
    kubernetesProvider: EKS
    controlPlaneTolerations: # if you need taint/toleration.
        - key: Management
        value: Tools
        effect: NoSchedule
    ```

5. install calico using helm

    ```powershell
    helm install calico projectcalico/tigera-operator --version v3.21.4 --namespace calico-system -f values.yaml
    ```