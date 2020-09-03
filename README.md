# helm-test

This is a demo of pushing a Helm Chart to the GitHub Container Registry https://ghcr.io/.

## Login

Currently the GHCR requires a [PAT](https://github.com/settings/tokens) with `read:packages` and `write:packages` scopes for authentication.

```shell
# After creating a PAT it will be in your clipboard, use pbpaste to set it.
export PAT=`pbpaste`

# ensure the required environment variable is set (only required once)
export HELM_EXPERIMENTAL_OCI=1

echo "$PAT" | helm registry login -u $USER https://ghcr.io --password-stdin 
```

## Add Stable

Regular helm commands to add a stable repo.

```shell
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm search repo stable
```

## Add Staging

Add GHCR as your staging repo

```shell
helm repo add staging https://ghcr.io
```

## Create Chart

Create a test Helm Chart! https://helm.sh/docs/helm/helm_create/

```shell
helm create helm-test
```

## Package Chart

Package up the Chart https://helm.sh/docs/helm/helm_package/

```shell
helm package ./helm-test 
```

## Save Chart

Similar to `docker tag` https://helm.sh/docs/topics/registries/#save

```shell
# ensure the required environment variable is set (only required once)
export HELM_EXPERIMENTAL_OCI=1

helm chart save helm-test/ ghcr.io/president-business-corp/helm-test:latest
```

## Push Chart

Similar to `docker push`  https://helm.sh/docs/topics/registries/#push

```shell
# ensure the required environment variable is set (only required once)
export HELM_EXPERIMENTAL_OCI=1

helm chart push ghcr.io/president-business-corp/helm-test:latest

```

## List Charts

Similar to `docker images` https://helm.sh/docs/topics/registries/#list

```shell
# ensure the required environment variable is set (only required once)
export HELM_EXPERIMENTAL_OCI=1

helm chart list

REF                                             	NAME   	VERSION	DIGEST 	SIZE   	CREATED  
ghcr.io/president-business-corp/helm-test:latest	mychart	0.1.0  	308d229	3.5 KiB	8 minutes
```

## Remove Chart

Similar to `docker rmi` https://helm.sh/docs/topics/registries/#remove

```shell
# if you haven't set this env you'll need it
export HELM_EXPERIMENTAL_OCI=1

helm chart remove ghcr.io/president-business-corp/helm-test:latest
```

## Pull

Similar to `docker pull` https://helm.sh/docs/topics/registries/#pull

```shell
# if you haven't set this env you'll need it
export HELM_EXPERIMENTAL_OCI=1

helm chart pull containers.pkg.github.com/president-business-corp/helm-test:latest  
```

## Setup

Here are some quick setup steps

### Install

You'll need a recent version of the `helm` command installed.

#### MacOS

```shell
brew install helm
```

## Environment Variable

You'll receive the following error using helm charts and an OCI registry if you don't set this environment variable. You only need to set this once per shell session but I've listed it with every instruction to ensure fewer mistakes.

`Error: this feature has been marked as experimental and is not enabled by default. Please set HELM_EXPERIMENTAL_OCI=1 in your environment to use this feature`

```shell
export HELM_EXPERIMENTAL_OCI=1 
```
