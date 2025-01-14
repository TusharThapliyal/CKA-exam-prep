# CKA-exam-prep

I will be using kind cluster with two worker node and a master node. All these nodes will be running as docker container on my machine.

I have two users:  
1. admin
2. tushar 

took below steps to configure .kube/config for tushar
1. `openssl genrsa -out tushar.key 2048` will create `tushar.key` file
2. `openssl req -new -key tushar.key -out tushar.csr -subj "/CN=tushar/O=tushar"`  here tushar is the user and group. this will create a `tushar.csr` 
3. find the ca.crt and ca.key in your control plane and copy them to your machine. If you are using minikube or kind cluster then use `docker cp` command to copy it from `/etc/kubernetes/pki`
4. `openssl x509 -req -in tushar.csr -CA ~/.kube/ca.crt -CAkey ~/.kube/ca.key -CAcreateserial -out tushar.crt -days 365` This will create a `tushar.crt`. these credentials will expire in 365 days.
5. you have to base-64 encode `tushar.crt` and `tushar.key` 
6. `kubectl config use-context uat-tushar` 
7. `kubectl config get-contexts` to check you current-context, user, cluster and namespace for `kubectl`.

I was using a single server with two users (ubuntu and tushar), both with different .kube/config files. 


