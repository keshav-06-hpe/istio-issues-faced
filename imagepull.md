Error came for no image pull so got help from Anand regarding the file<br>
We Downloaded the image from the artifactory to local system using following script:
```sh
NEXUS_USERNAME="$(kubectl -n nexus get secret nexus-admin-credential --template {{.data.username}} | base64 -d)"
 
NEXUS_PASSWORD="$(kubectl -n nexus get secret nexus-admin-credential --template {{.data.password}} | base64 -d)"
 
IMAGE=""
 
ARTIFACTORY_USER=""
ARTIFACTORY_TOKEN=""
 
podman run -v ./dir:/images --rm --network host quay.io/skopeo/stable copy --src-tls-verify=false --src-creds "${ARTIFACTORY_USER}:${ARTIFACTORY_TOKEN}" --dest-creds "${NEXUS_USERNAME}:${NEXUS_PASSWORD}" --dest-tls-verify=false docker://artifactory.algol60.net/$IMAGE docker-archive:/images/sma-rsyslog.tar

podman run  -v ./dir:/images --rm --network host quay.io/skopeo/stable copy --src-tls-verify=false --src-creds "${ARTIFACTORY_USER}:${ARTIFACTORY_TOKEN}" --dest-creds "${NEXUS_USERNAME}:${NEXUS_PASSWORD}" --dest-tls-verify=false docker-archive:/images/sma-rsyslog.tar docker://registry.local/artifactory.algol60.net/$IMAGE
```
