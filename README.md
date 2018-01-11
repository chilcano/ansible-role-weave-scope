# Ansible Role: Weave Scope

An Ansible Role that deploys Weave-Scope (https://github.com/weaveworks/scope) in an OpenShift cluster running locally, generally created by using Minishift (https://www.openshift.org/minishift).

Weave Scope is a Monitoring, visualisation & management Tool for Docker & Kubernetes.
For further details here: https://github.com/weaveworks/scope

This Role performs the following tasks:

- Check if OpenShift is running locally.
- Installs from Internet or local.
- Uses the latest `oc` binary from `~/.minishift/cache/oc/<VERSION>/<OS>/` to deploy Weave Scope.

## Observations

The Weave Scope Ansible Role has been tested with:
- Ansible 2.3+
- minishift v1.11.0+4459917
- VirtualBox 5.1.30
- macOS High Sierra, version 10.13.2 (17C88)
- Prior to running the role, clear your terminal session of any DOCKER* environment variables.
- Weave Scope requires access to OpenShift running locally and an `system` account. If you want to get an OpenShift instance running locally, please, see `https://galaxy.ansible.com/chilcano/minishift` to get a VM with OpenShift.

## Default Role variables

The default variables are in `defaults/main.yml`.

## Example Playbook

See `sample-1-weave-scope.yml` file for an example.

## Using the Ansible Role

Install the role:
```
$ sudo ansible-galaxy install chilcano.weave-scope
```

Copy the playbook from your roles path to the current working directory:
```
$ cp ${ANSIBLE_ROLES_PATH}/chilcano.weave-scope/sample-1-weave-scope.yml .
```

Create an `inventory` file
```
$ echo $(hostname) > ./inventory
```

Run the playbook:
```
$ ansible-playbook -i inventory --ask-become-pass sample-1-weave-scope.yml
```

In order to get access to Weave Scope from browser, we should forward the Weave Scope's port (`4040`) to the Host. In other words we have to execute this command:
```
$ oc port-forward -n weave-scope "$(oc get -n weave-scope pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')" 4040
```

Once done, open your browser with this URL and you could visualize all Pods, Containers, Controllers, etc. of your OpenShift Cluster.


* Exploring OpenShift with Weave Scope.

![Exploring OpenShift with Weave Scope](https://github.com/chilcano/ansible-role-weave-scope/blob/master/imgs/api-mesh-security-2-weave-scope.png "Exploring OpenShift with Weave Scope")


* Exploring in depth the API Mesh.

![Exploring in depth the API Mesh](https://github.com/chilcano/ansible-role-weave-scope/blob/master/imgs/api-mesh-security-9-weave-scope-bookinfo-mesh.png "Exploring in depth the API Mesh")


## License

MIT / BSD

## Author Information

This role was created in 2017 by [Roger Carhuatocto](https://www.linkedin.com/in/rcarhuatocto), author of [HolisticSecurity.io Blog](https://holisticsecurity.io).
