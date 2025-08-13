## Secret management with Google Cloud Secret Manager in Kubernetes

- Step 1: Create a secret in Google Cloud Secret Manager.


```bash

echo -n "SuperSecretPassword" | gcloud secrets create db-password --data-file=-

```


- Step 2: Grant Kubernetes service account access to the secret.



- Step 3: Use the secret in your Kubernetes pods.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
    containers:
    - name: app-container
      image: your-app-image
      volumeMounts:
        - name: secret-volume
          mountPath: /etc/secrets
          readOnly: true
    volumes:
    - name: secret-volume
      secret:
        secretName: db-password  # Name of the secret in GCP Secret Manager

```