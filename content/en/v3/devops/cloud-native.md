---
title: Cloud Native
linktitle: Cloud Native
type: docs
description: Recomendações Cloud Native 
weight: 200
---

Uma das recomendações do [Accelerate](/v3/devops/accelerate/) é sobre usar nuvens bem; deixando os desenvolvedores usar nuvens para resolver porblemas de software. 

Aqui estão algumas das lições que aprendemos sobre usar bem nuvens.  
## Dê preferencia às nuvens do que kubernetes

Você pode fazer o deploy da base de dados via a helm chart no seu cluster de kubernetes. Ou  você pode configurar seu provedor de serviços em nuvem para criar um base de dados gerenciável. 

Você pode fazer o deploy, digamos,  [vault](https://www.vaultproject.io/) como helm charts  dentro do seu cluster de kubernetes. Ou você pode usar seu armazenamento secreto do provedor de serviços em nuvem como, por exemplo:

* Alibaba Cloud KMS Secret Manager
* Amazon Secret Manager
* Azure Key Vault
* GCP Secret Manager

Nós recomendamos que se você tiver escolha; vá com a versão em nuvem.

O motivo principal é que essas coisas são de toda forma trabalhosas. Seu provedor de serviços em nuvem pode instalar, atualizar, fazero backup e gerenciar esses serviços para você. 

Se você for com helm charts dentro do kubernetes então você precisa ter certeza de fazer o backup quer irá armazenar todos os dados  e testar seu backup e mecanismos de restauração. 
### Prefira banco de dados na nuvem

Seu provedor de serviços em nuvem pode lidar com backups, atualizações e escalabilidade para você.

### Prefira armazenamento secreto em nuvem  

Ao invés de instalar, atualizar, fazer o backup e gerenciar seu próprio Cofre

### Prefira resgidtros de container em nuvem 

Ao invés de instalar e gerenciar seu própio  nexus / artifactory / harbor / chart museuem

### Prefira serviços de  hospedagem de repositórios git

Ao invés de instalar e gerenciar seu própio gitlab / gitea / bitbucket server 

### Tente evitar Volumes Persistentes 

Similar do acima; se você usar armazenamento em nuvem, buckets em nuvem, registros de containers em nuvem você tem menos dados para fazer o backup pois o provedor do servicço em nuvem tipicamente já faz pra você. 

Lembre-se que o recurso de Volume Parsistente em kubernetes não são gratuitos; você precisa de fazer o backup e gerenciá-los.                                                     

## Trate clusters de kubernetes como gado não como animais de estimação

Se acusteme com a ideia que você pode deletar seu clusters de kubernetes a qualquer momento e recriá-lo rapidamente.  

e.g. to change region or machine type this will usually happen.


## Map IAM Roles to kubernetes Service Accounts

On AWS use [IAM roles for service accounts](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html) (IRSA)

On GCP use [Workload Identity](https://cloud.google.com/kubernetes-engine/docs/how-to/workload-identity) (WLI)

In both cases this maps cloud IAM roles to kubernetes `ServiceAccount` resources using annotations. 

This means that you don't have to populate your kubernetes cluster with cluster-admin style cloud IAM secrets - which makes your system more secure and reduces the possibility of accidentally exposing a secret.

Note that if you use [Jenkins X to configure your clusters with Terraform and GitOps](/v3/admin/) then you get this out of the box! 

## Terraform for cloud infrastructure

We are all using an increasing amount of cloud infrastructure. You can use your cloud providers CLI or web console to set things up. However it's hard to manage and version.

So we recommend the [GitOps approach](/v3/devops/gitops/) to all infrastructure; both cloud infrastructure and kubernetes charts, resources and configuration.

So to manage your infrastructure use a git repository with your [terraform](https://www.terraform.io/) configuration.

There is a catch 22 of how do you start to provision your first, say, kubernetes cluster using [terraform](https://www.terraform.io/) before you have any cloud infrastructure.

You could look at using [Terraform Cloud](https://www.terraform.io/cloud) as the place to setup your core cloud infrastructure.


## Try use the same GitOps approach everywhere

If you treat different clusters very differently in how you setup them up, install, upgrade, manage and monitor them you've given yourself more work to do and increase the changes of things going wrong or getting out of step.

So try using the same [GitOps approach](/v3/admin/guides/jenkins/gitops/) for all clusters in all environments.
