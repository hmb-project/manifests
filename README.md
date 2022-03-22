# manifests

manifests 会定期同步其上游仓库中的所有 HMB 组件。下列矩阵显示了HMB每个组件所对应的git版本。

| 组件 | 局部清单路径 | 上游版本 |
| - | - | - |
| Training Operator | apps/training-operator/upstream | [v1.3.0](https://github.com/kubeflow/tf-operator/tree/v1.3.0/manifests) |
| MPI Operator | apps/mpi-job/upstream | [v0.3.0](https://github.com/kubeflow/mpi-operator/tree/v0.3.0/manifests) |
| Notebook Controller | apps/jupyter/notebook-controller/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/notebook-controller/config) |
| Tensorboard Controller | apps/tensorboard/tensorboard-controller/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/tensorboard-controller/config) |
| Central Dashboard | apps/centraldashboard/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/centraldashboard/manifests) |
| Profiles + KFAM | apps/profiles/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/profile-controller/config) |
| PodDefaults Webhook | apps/admission-webhook/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/admission-webhook/manifests) |
| Jupyter Web App | apps/jupyter/jupyter-web-app/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/crud-web-apps/jupyter/manifests) |
| Tensorboards Web App | apps/tensorboard/tensorboards-web-app/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/crud-web-apps/tensorboards/manifests) |
| Volumes Web App | apps/volumes-web-app/upstream | [v1.4.0](https://github.com/kubeflow/kubeflow/tree/v1.4.0/components/crud-web-apps/volumes/manifests) |
| Katib | apps/katib/upstream | [v0.12.0](https://github.com/kubeflow/katib/tree/v0.12.0/manifests/v1beta1) |
| KFServing | apps/kfserving/upstream | [v0.6.1](https://github.com/kubeflow/kfserving/releases/tag/v0.6.1) |
| Kubeflow Pipelines | apps/pipeline/upstream | [1.7.0](https://github.com/kubeflow/pipelines/tree/1.7.0/manifests/kustomize) |
| Kubeflow Tekton Pipelines | apps/kfp-tekton/upstream | [v1.0.0](https://github.com/kubeflow/kfp-tekton/tree/v1.0.0/manifests/kustomize) |

## 使用方法

Manifests 工作组为使用kustomize安装HMB提供了两个选项，其目的是为了帮助用户轻松安装。

### 环境准备

Kubernets集群（Kubernetes version需为 v1.19.x ～ v1.20.x）并且设置了[默认存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)
   
   ```shell
   kubectl patch storageclass <your-class-name> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
   ```
HMB 目前与最新版本 kustomize不兼容,需要下载 kustomize v3.2.0。 
   ```shell
  curl -LO https://github.com/kubernetes-sigs/kustomize/releases/download/v3.2.0/kustomize_3.2.0_linux_amd64
   ```
 
如果未安装 kubectl，请下载kubectl。版本需要与集群版本一致，请修改下载地址的版本号。
   
   ```shell
  curl -LO https://dl.k8s.io/release/v1.20.6/bin/linux/amd64/kubectl
   ```


### 安装

你可以下述命令安装所有位于HMB官方组件，这将会创建一个 HMB demo：

```sh
while ! kustomize build demo | kubectl apply -f -; do echo "Retrying to apply resources"; sleep 10; done
```
