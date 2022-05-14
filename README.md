
## About

Kubernetes 리소스를 만들기 위한 여러 예제들을 작성합니다.

Kubernetes 리소스를 필요로할 때 해당 예제들을 참조/조합하여 빠르게 만들 수 있도록 합니다.

## Tools

Kubernetes 클러스터를 관리할 때 유용한 툴들을 설치하여 사용합니다.

### Chocolatey

Windows OS를 위한 Package Manager입니다. 다양한 툴들을 명령줄을 통해 간단하게 설치할 수 있습니다.

- Install Chocolatey on powershell(run as administrator)
    ```powershell
    # REF: 
    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
    ```

### kubectl

kubectl을 통해 api server로 리소스 생성, 수정, 삭제 등의 원하는 요청을 보낼 수 있습니다.

Windows

- Install kubectl

    ```powershell
    # REF : https://kubernetes.io/ko/docs/tasks/tools/install-kubectl-windows/
    choco install kubernetes-cli
    ```

### eksctl

eksctl을 사용하면 EKS 클러스터, 관리형 노드그룹, IRSA 등의 AWS 관련 리소스 관리 작업을 간단한 명령줄로 수행할 수 있습니다.

Windows

- Install eksctl on powershell(run as administrator)
    
    ```powershell
    choco install -y eksctl 
    ```

### Helm3

aws-load-balancer-controller, metrics-server와 같은 컨트롤러는 이미 작성된 Public Helm Chart를 활용하여 손쉽게 배포할 수 있습니다.

Windows

- Install Helm3 on powershell(run as administrator)

    ```powershell
    # REF : https://helm.sh/ko/docs/intro/install/
    choco install kubernetes-helm
    ```

### k9s

k9s를 사용하면 terminal UI를 통해 쿠버네티스 리소스 및 클러스터를 관리할 수 있습니다.

Windows

- Install k9s on powershell(run as administrator)

    ```powershell
    choco install k9s
    ```