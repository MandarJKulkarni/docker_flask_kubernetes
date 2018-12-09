This is to demonstrate how to create a docker image for simple Flask app
and deploy it on Kubernetes

Commands to build docker image, tag it, push it
	docker build -t flaskapp .
	docker tag flaskapp gcr.io/<GCP project ID>/flaskapp
	docker push gcr.io/data-ecosystem/flaskapp


Then deploy it on k8s
	kubectl run flaskapp --image=gcr.io/<GCP project ID>/flaskapp --port 8080
	kubectl expose deployment flaskapp --type=ClusterIP --port 8080 --target-port 8080