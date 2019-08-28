
# Semantic Kubernetes

## Problem

- Orchestration solutions usually have **a lot** of different mechanisms for
  things like _resource allocation_ and _deployment order_.
- It is very likely that at least one of these mechanisms is **not a good fit**.
- Orchestration may need more information to make good decisions.

⇒ We built around **Nomad**'s orchestration mechanisms
  (and nearly Kubernetes')

> Wouldn't it be great if you could "encode" domain semantics into Kubernetes?

**You can!**
