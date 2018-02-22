# graftM-docker

## Building
GraftM docker images are now generated through GNU Guix, so building them from a Dockerfile is no longer necessary or supported. To procure the GraftM image:
```
docker pull wwood/graftm:<version>
```
Where `<version>` is the desired version e.g. `v0.11.1`.

### Old versions 0.9.4 and before
To build the docker image, please ensure the "resources" file is in your current working directory (best to copy the whole version directory from git) and run:
```
docker build -t Dockerfile .
```

## Running
**The easy way** to run the graftm docker - The most simple way to use the GraftM docker image is to  move all the files GraftM needs to access to the current working directory, and use for example the following command:

```
docker run -u $(id -u):$(id -g) -v `pwd`:/data wwood/graftm:v0.11.1 graft <options>
```

**The hard way** to run the graftm docker - If you wish to specify a reads file or gpkg that is **not** in the current working directory you will need to mount the path to each file to the image using the -v command as done above, **and** specify the local directory for the file to the GraftM command. For example if I wanted to use a gpkg not in the current directory:

```
docker run -u $(id -u):$(id -g) -v `pwd`:/data -v /path/to/my_gpkg.gpkg:/gpkg wwood/graftm:v0.11.1 graft --forward <my_reads.fa> --graftm_package /gpkg/<my_gpkg.gpkg>
```

We recommend the easier way.
If you still wish to run using files not in the current working directory, please mount each type of data to the correct directory within the image:
* GraftM packages (gpkg) --> **gpkg** (e.g. ```-v /path/to/gpkg:/gpkg```)
* Sequence data --> **reads** (e.g. ```-v /path/to/reads:/reads```)
* Specific search HMM  --> **hmm** (e.g. ```-v /path/to/hmm:/hmm```)

This image is quite large, due to the number of dependencies required to run GraftM - apologies for that. Please do drop a message here on the GitHub page if you have any questions or concerns.
