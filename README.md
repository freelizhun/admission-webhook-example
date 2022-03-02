# Kubernetes Admission Webhook example

This tutoral shows how to build and deploy an [AdmissionWebhook](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks).

The Kubernetes [documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/) contains a common set of recommended labels that allows tools to work interoperably, describing objects in a common manner that all tools can understand. In addition to supporting tooling, the recommended labels describe applications in a way that can be queried.
In our validating webhook example we make these labels required on deployments and services, so this webhook rejects every deployment and every service that doesn’t have these labels set. The mutating webhook in the example adds all the missing required labels with `not_available` set as the value.

## Prerequisites

Kubernetes 1.9.0 or above with the `admissionregistration.k8s.io/v1beta1` API enabled. Verify that by the following command:
```
kubectl api-versions | grep admissionregistration.k8s.io/v1beta1
```
The result should be:
```
admissionregistration.k8s.io/v1beta1
```

In addition, the `MutatingAdmissionWebhook` and `ValidatingAdmissionWebhook` admission controllers should be added and listed in the correct order in the admission-control flag of kube-apiserver.

## Build

Build and push docker image
   
```
./build
```

## How does it work?

We have a blog post that explains webhooks in depth with the help of this example. Check [it](https://www.qikqiak.com/post/k8s-admission-webhook/) out!

## 另外一个关于`ValidatingAdmissionWebhook`例子
请[参考](https://docs.giantswarm.io/advanced/custom-admission-controller/)

## ingressClass
ingressclass概念：
* 安装Ingress Controller 时可以指定参数 -ingress-class <string > ，默认是nginx
* 这个参数指定的就是这个ingress控制器是属于那个IngressClass
* 当创建一个ingress时，通过 spec.ingressClassName: <string > 来指定这个ingress属于那个IngressClass，属于那个ingress控制器
* 在IngressClass资源上将annotations ingressclass.kubernetes.io/is-default-class设置 为true，将确保未指定ingressClassName新的Ingress分配此默认值IngressClass。
