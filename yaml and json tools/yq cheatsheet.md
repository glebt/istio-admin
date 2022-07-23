```bash

#single volume
yq '.spec.volumes[] | select(.name == "podinfo")' ingress.yaml

#select secrets only
yq '.spec.volumes[] | select(.secret?)' ingress.yaml

#anything that has secret property
yq '.. | select(.secret?)' ingress.yaml


#two volumes to array
yq '.spec.volumes[] | select(.name == "podinfo" or .name == "config-volume") | [{"volume": .}]' ingress.yaml
```
