#INSTALL GATEKEEPER
kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/master/deploy/gatekeeper.yaml

#INSTALL TEMPLATE Resource Limit
kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper-library/master/library/general/containerlimits/template.yaml

#INSTALL TEMPLATE Privileged Container
kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper-library/master/library/pod-security-policy/privileged-containers/template.yaml

#Upload Policy ke OPA
curl -X PUT http://<EXTERNAL-IP>:8181/v1/policies/example \
  -H "Content-Type: text/plain" \
  --data-binary @policy.rego

#Basic Authorization Allowed
curl -X POST http://<EXTERNAL-IP>:8181/v1/data/example/allow \
  -d '{"input": {"user": "nita"}}'

#Basic Authorization Denied