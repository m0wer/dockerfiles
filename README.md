This repo contains various Dockerfiles I use on the desktop and on servers.
It's similar to [jessfraz/dockerfiles](https://github.com/jessfraz/dockerfiles)

# Building the images

To build all the images without using build cache and using `n_jobs` parallel
threads, and then push them to `{registry_url}` do

```bash
REPO_URL={repo_url} JOBS={n_jobs} NO_CACHE=TRUE sh -c ./build-all.sh
```

The images will be tagged as `{registry_url}/{directory_name}:latest`, where
`directory_name` is the name of the directory containing the *Dockerfile*.
