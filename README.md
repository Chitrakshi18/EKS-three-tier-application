Enhancements:
1. Configured EBS CI driver for leveraging peristent volume for mongodb database
Create an IAM role and attach a policy. AWS maintains an AWS managed policy or you can create your own custom policy.

eksctl create iamserviceaccount \
    --name ebs-csi-controller-sa \
    --namespace kube-system \
    --cluster <YOUR-CLUSTER-NAME> \
    --role-name AmazonEKS_EBS_CSI_DriverRole \
    --role-only \
    --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
    --approve

2. Run the following command
eksctl create addon --name aws-ebs-csi-driver --cluster <YOUR-CLUSTER-NAME> --service-account-role-arn arn:aws:iam::<AWS-ACCOUNT-ID>:role/AmazonEKS_EBS_CSI_DriverRole --force

3. Added mongo-pvc.yaml file
   
4. Changed mongo/deploy.yaml from deploymnent to StatefulSet resource.
5. Implemented Automated Synchronization with Argo CD
6. Install argoCD
   
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

7. Expose Argo CD Server Service in NodePort Mode
kubectl edit svc argocd-server -n argocd
(and change the type to NodePort from ClusterIP)

8. Create application which points to this repo url
   
