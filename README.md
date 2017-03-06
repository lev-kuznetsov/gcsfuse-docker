# gcsfuse-docker

Docker image for mounting GCS buckets. Container must be started as privileged for mount to succeed. Service account credentials will be picked up at `/etc/gcloud/service-account.json`. The easiest way to use this to mount a single bucket would be to extend this image, add the service account credentials file you get from Google cloud console and use the `gcsfuse` mount command directly:

```
FROM levkuznetsov/gcsfuse-docker

ADD service-account.json /etc/gcloud/service-account.json

CMD ["gcsfuse", "--foreground", "-o", "allow_other", "BUCKET-NAME", "/mnt"]
```

Do not push any images containing your service account credentials to any public repository!
