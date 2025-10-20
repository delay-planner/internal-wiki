# Podman Loading

```
podman commit IMAGE_NAME kirk-img:latest
podman save -o kirk_img.tar kirk-img:latest

podman load -i kirk_img.tar
podman run -it localhost/kirk-img:latest /bin/bash
```
