This is to demonstrate how to create a docker image for simple Flask app
and deploy it on Kubernetes

Requirements:
	Have Docker and kubernetes installed.

Commands to build docker image, tag it, push it
	
	docker build -t flaskapp .
	
	docker tag flaskapp gcr.io/<GCP project ID>/flaskapp
	
	docker push gcr.io/data-ecosystem/flaskapp


Then deploy it on k8s
	
	kubectl run flaskapp --image=gcr.io/<GCP project ID>/flaskapp --port 8080
	
	kubectl apply -f .\flaskapp-withproductpage-svc.yml
	
Check the app is running by clicking on the load balancer service in K8S cluster

For Istio:

If you are deploying on a kubernetes cluster which has Istio, then you need to expose the deployment as ClusterIP
	
	kubectl expose deployment flaskapp --type=ClusterIP --port 8080 --target-port 8080
	
Apply the gateway, virtual service for the app.
	
	kubectl apply -f flask-productpage-gateway-vsvc.yml
Add the service entries for google.com and time.jsontest.com

	kubectl apply -f google-serviceentry.yml
	kubectl apply -f time-jsontest-serviceentry.yml
