# Config Map via Config File.

### Create

```sh
kubectl create configmap [NAME]--from-file [/PATH/TO/FILE.PROPERTIES] --from-file [/PATH/TO/FILE2.PROPERTIES]

```

```sh
kubectl create configmap [NAME]--from-file [/PATH/TO/FILE.PROPERTIES] --from-file [/PATH/TO/DIR]
```

> example :

### Get

```sh
kubectl get configmap [NAME] -o yaml/json
```

# Secrets

it should not have $ ! * \
then --> it needs escaping

```sh
kubctl get secrets
```
```sh
kubctl describe secrets <Sec. Name>
```