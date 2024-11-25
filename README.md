# ansible-kubernetes
ansible dev container with k3d, helm and kubectl

TLDR;

```
pip install -r requirements.txt
ansible-playbook playbook.yml
kubectl get pods
```

Then with the 0th pod do:

```
kubectl -n default port-forward svc/wordpress 8080:80
kubectl -n default port-forward svc/jaeger-jaeger-all-in-one 16686:16686
```

This is a group assignment. The assignment is to run the worked example and answer some questions in a word document. The marking scheme is:

|item|up to|
|--|--|
|produce a deployment diagram that shows all of the services|10|
|choose a trace request and describe what you see|5|
|find an error and state the status_code|5|
|summarize your observations in a few paragraphs|5|
|total|25|

Wordpress is a monolith application. Hopefully you can see how monitoring, tracing and logging add to it's maintainability.


