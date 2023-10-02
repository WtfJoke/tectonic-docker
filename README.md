![docker pulls](https://img.shields.io/docker/pulls/dxjoke/tectonic-docker.svg)
# Docker Tectonic with Biber 
A tiny docker image with a working [tectonic latex
engine](https://tectonic-typesetting.github.io/en-US/index.html) and [biber](https://github.com/plk/biblatex) with a primed cache.

* Visit my page on docker hub at: https://hub.docker.com/r/dxjoke/tectonic-docker/
* Visit my page on github at: https://github.com/WtfJoke/tectonic-docker


## Getting the image
```
docker pull dxjoke/tectonic-docker
```

Only **~75MB** compressed.

A fully working latex engine. Packages that are not in the cache will be
downloaded on demand.


# Github
In case you want to use this docker image in github.
</br>
Please check out and use my github action [WtfJoke/setup-tectonic](https://github.com/WtfJoke/setup-tectonic) instead. 

The action performs better and supports individual caching (:zap:) of your downloaded tex packages.

# Example: Gitlab CI

Create a `.gitlab-ci.yml` with the following content for very fast
pdf builds.

```yaml
pdf:
  image: dxjoke/tectonic-docker
  script:
    - tectonic --keep-intermediates --reruns 0 main.tex
    - biber main
    - tectonic main.tex
  artifacts:
    paths:
      - main.pdf
```

## Example: Gitlab CI (without biber)
In case you dont need biber, you simply ommit the first two script calls. Eg.

```yaml
pdf:
  image: dxjoke/tectonic-docker
  script:
    - tectonic main.tex
  artifacts:
    paths:
      - main.pdf
```

### Priming the cache

After building tectonic, it is run on the tex files in this repo to
download all the common files from the tectonic bundle. These files are bundled in the docker image

## Running locally
On windows:

`docker run -it -v c:/mytex/folder/thesis:/data dxjoke/tectonic-docker`

On linux:

`docker run -it -v /home/user/mytex/folder/thesis:/data dxjoke/tectonic-docker`

Afterwards you can cd into /data and run tectonic/biber as you wish.
Eg:
```
cd /data
tectonic --keep-intermediates --reruns 0 main.tex
biber main
tectonic main.tex
```

