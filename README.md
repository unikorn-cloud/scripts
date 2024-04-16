# Unikorn Scripts

![Unikorn Logo](https://raw.githubusercontent.com/unikorn-cloud/assets/main/images/logos/light-on-dark/logo.svg#gh-dark-mode-only)
![Unikorn Logo](https://raw.githubusercontent.com/unikorn-cloud/assets/main/images/logos/dark-on-light/logo.svg#gh-light-mode-only)

Useful shiz for developing Unikorn.

## Prerequisites

* GNU `make`
* `go`
* `kubectl`
* `jq`
* `yq`

## Scripts

### build

Most useful script, this builds the binaries on your local machine, tags them with the most recent version defined in the Helm chart, and pushed them into KinD.

### deploy

Second most useful script, this deploys the component to KinD.
You will need to provide Helm values files to override default behaviour, which will be broken.
Only restarts all services if the Helm chart version has changed, or their pod templates have.

### restart

Like `deploy`, but just deletes all the pods.
This is used when a deploy would do nothing, e.g. the pod images or arguments have't changed but you have a new functional change pushed with `build`.

### ui-preview

UI developer mode script, which has live reload and debug information readily available in your browser.
You will need to define a few environment variables for your setup, see the code of details.

### clean-images

Docker images are big, and if you are compiling 20 a day, that's a lot of space.
This deletes any danging images.

## Typical Usage

Fresh install:

```shell
build && deploy
```

Test a functional change:

```shell
build && restart
```

## Installation

Run:

```shell
make install
```

**NOTE**: This defaults to ~/bin, you can set `PREFIX` to modify this.

## Contribution

Be aware you need to run `shellcheck` and pass before acceptance.
