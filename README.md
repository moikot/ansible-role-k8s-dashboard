# Ansible Role: Kubernetes Dashboard

An Ansible role that installs [Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) and allows you to change default arguments and cluster role binding.

**NOTE:** This Ansible role intended to be used for home experiments only.

## Requirements

Requires Kubernetes and `kubectl`.

## Role variables

Link to the Dashboard manifest:

    k8s_dashboard_manifest: https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta2/aio/deploy/recommended.yaml

Dashboard arguments:

    k8s_dashboard_args:
      - --auto-generate-certificates
      - --namespace=kubernetes-dashboard

Dashboard cluster role reference:

    k8s_dashboard_cluster_role: kubernetes-dashboard

## Playbook example

**IMPORTANT:** This example granting admin privileges to Dashboard's service account and allows you to skip authorization. Please read [Access control](https://github.com/kubernetes/dashboard/wiki/Access-control) Wiki before using it.

```yaml
- hosts: all

  vars:
    k8s_dashboard_cluster_role: cluster-admin  

    k8s_dashboard_args:
      - --enable-skip-login
      - --disable-settings-authorizer
      - --auto-generate-certificates
      - --namespace=kubernetes-dashboard

  roles:
    - moikot.k8s-dashboard
```
