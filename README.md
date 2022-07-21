Quite recently, I was tasked with creating a production ready Kubernetes cluster from the ground up at [Darey.io](https://www.darey.io/) where I Learn DevOps via a Project Based Learning model. This task gave me a deep and practical insight into the technical structure and setup of Kubernetes. Though it took me a while, I was able to set it up as requested and as per documentation. 

Moving forward with the knowledge gained, I decided to set up an AWS EKS Cluster which I would use for some application deployments. This next tasks would center around deployments and persisting data in k8s. However, this article is only a guide to provisioning your own [AWS EKS Cluster](https://docs.aws.amazon.com/eks/latest/userguide/clusters.html) using IaC(Terraform). It is advisable to do this first with the console if you don't already have knowledge as to how it all works. 

Terraform is the IaC tool for this guide(knowledge of terraform is a prerequisite for this process), below are the steps to follow in setting up your EKS Cluster using terraform on your control machine;

1. Setup a controller client machine(can be an EC2 instance or your local machine)
2. Install [Terraform](https://www.terraform.io/downloads), [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/), [AWSCLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html), [aws-iam-authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)
3. Create a folder where you'd clone the Terraform repo already provide by Hashicorp/AWS ![repo](https://community.ops.io/remoteimages/uploads/articles/kuf9ea648vgt90zi7dho.png)

4. Clone down the [Github Repo] (https://github.com/hashicorp/terraform-provider-aws) into your controller client machine ![repo clone](https://community.ops.io/remoteimages/uploads/articles/1cazzf34umw4hys4yazh.png)

5. `cd` into the folder, `cd` into examples dir, `cd` into eks-getting-started ![Image](https://community.ops.io/remoteimages/uploads/articles/br9clb9uk03cm3xg1i2b.png)

6. `ls` to see the '.tf' files ![tf files](https://community.ops.io/remoteimages/uploads/articles/57ozv1gowydmw5l5ywpq.png)

7. Feel free editing to your preference, things such as Region, names, instance type for the worker nodes, version of Kubernetes among others.

8. Run `terraform init` to initialize the folder, `terraform plan` to see what resources would be created. 18 resources would be created in building this cluster. `terraform apply` to create the resources. It would take some 8-10 min for the cluster to be built and ready to go. ![Init](https://community.ops.io/remoteimages/uploads/articles/lulygg1oqgm9u5e2adyb.png) ![apply](https://community.ops.io/remoteimages/uploads/articles/me109xs1918sqfwnlqgs.png)

9. Now the cluster is built, you have to update the --kubeconfig with the awscli command 
```
aws eks --region <region> update-kubeconfig --name <cluster-name>
```
![kubeconfig](https://community.ops.io/remoteimages/uploads/articles/6ggtgd8gvkur9bjdgkxg.png) 

10. Test that everything works by running a `kubectl` command(any kubectl command) to show the nodes in your cluster

```
kubectl get nodes -o wide
``` 
 ![get-nodes](https://community.ops.io/remoteimages/uploads/articles/zyi3o3beuthmis97w6ns.png)



