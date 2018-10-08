# How to setup NFS Persitent Volume in OpenShift

## Pre-requisites
- Setup you OpenShift cluster using this project

https://github.com/corpbob/openshift_ansible_vagrant

## Steps
1. Clone this repository

```
git clone https://github.com/corpbob/openshift_nfs_ansible.git
```
2. Edit the file nfs_pvc.yml. Modify the variable max_pv to a value you want. The default is 2.

3. Run the ansible-playbook

```
ansible-playbook -i hosts nfs_pvc.yml
```

## Test it.
1. Create a new project

```
oc new-project test
```

2. Deploy a postgresql database

```
oc new-app postgresql-persistent -p POSTGRESQL_USER=admin -p POSTGRESQL_PASSWORD=admin
```

3. Verify that the database is using the persistent volume, for example:

```
oc get pvc

NAME      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM              STORAGECLASS   REASON    AGE
pv0       5Gi        RWO            Recycle          Bound       test/postgresql 

```
