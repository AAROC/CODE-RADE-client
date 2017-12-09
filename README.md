[![Docker Repository on Quay](https://quay.io/repository/aaroc/code-rade-client-centos7/status "Docker Repository on Quay")](https://quay.io/repository/aaroc/code-rade-client-centos7) [![Build Status](https://ci.sagrid.ac.za/job/execution containers/badge/icon)](https://ci.sagrid.ac.za/job/execution containers)

# CODE-RADE-client

Container to use CODE-RADE, built with [Ansible-Container](https://docs.ansible.com/ansible-container)

## About

This is a container-ready Ansilbe project, which is designed to use the [CODE-RADE application repository](http://www.africa-grid.org/CODE-RADE). 
CODE-RADE publishes pre-built and tested scientific applications to a [CVMFS](http://cvmfs.readthedocs.io/en/stable/) repository.
It applies the [cvmfs-client-2.2](https://github.com/AAROC/cvmfs-client-2.2) role - typically from [Ansible Galaxy](https://galaxy.ansible.com/AAROC/cvmfs-client-2-2/).
Containers are built and pushed to the [Quay  registry](https://quay.io/repository/aaroc/code-rade-client-centos7).

## Building 
If you would like to build, extend or fork the containers, you will need Ansible Container available locally : 

```
virtualenv coderade
source  coderade/bin/activate
pip install ansible-container[docker]
ansible-container build
```

## Using

The containers are automatically built by [Jenkins](https://ci.sagrid.ac.za/view/Infrastructure/job/execution containers/) and pushed to Quay. They can be simply pulled and used standalone, or deployed against your cloud platform (Kubernetes or OpenShift)

### Docker 

Although this project is designed to be used in a cloud environment, it can be run standalone using docker. Note that since the container needs to mount a FUSE filesystem (CVMFS), it needs to be run privileged:

```
docker pull quay.io/aaroc/code-rade-client-centos7
docker run --privileged -ti quay.io/code-rade-client-centos7 /bin/bash -c 'mount -a ; cat /cvmfs/code-rade.africa-grid.org/version`
```

This should display the version of the repository and the job which triggered it.

### Ansible Container

You can run the containers locally using a Docker instance, once they have been built.

```
ansible-container run 
```


# References

- Bruce Becker, & Sean. (2017, August 4). AAROC/cvmfs-client-2.2: CODE-RADE cvmfs client role v1.1.2 Zenodo. http://doi.org/10.5281/zenodo.596013