docker run -i --rm quay.io/coreos/mkpasswd --method=yescrypt
docker run -i --rm quay.io/coreos/fcct --pretty --strict < ignition.yaml > ignition.ign
docker run -i --rm quay.io/coreos/ignition-validate - < ignition.ign
