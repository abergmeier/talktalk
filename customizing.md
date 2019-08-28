
# Semantic Kubernetes

## Customizing

> How do I teach Kubernetes my domain semantics (to a certain degree)?

### Custom (API) resources

See https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources
> Custom resources are extensions of the Kubernetes API. This page discusses when to add a custom resource to your Kubernetes cluster and when to use a standalone service. It describes the two methods for adding custom resources and how to choose between them.

This introduces the **definitions**. The schema definition for a CR is called _**C**ustom**R**esource**D**efinition_.

CRD example:


### Custom Controllers

It is possible to write your own controllers, which reconciles depending on
updated API resources and/or external state.

Controller example:

### Operators

_Operator_ pattern is a combination of _Custom resources_ and _Controllers_.
With these concepts it is possible to extend Kubernetes with domain semantics.

https://coreos.com/blog/introducing-operators.html

**Implementing Operators**

> How is this done in practise?

Options for implementing are:
- **DIY**

  Write all communication with the Kubernetes API and state yourselfes.
- **[Kubebuilder](https://github.com/kubernetes-sigs/kubebuilder)**

  > Kubebuilder is a framework for building Kubernetes APIs using custom resource definitions (CRDs).

- **[Operator SDK](https://github.com/operator-framework/operator-sdk)**

  > The Operator SDK is a framework that uses the controller-runtime library to make writing operators easie

  Opinionated generator suite for introducing CRDs and Controllers.

- **[KUDO](https://kudo.dev)**

  Operator, which can by configured using YAML and predefined actions.

> What about third-party operators?

See https://operatorhub.io/.


