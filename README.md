# graftM-docker
docker images for GraftM

To build the docker image:
```
docker build -t Dockerfile .
```

**The easy way** - The most simple way to use the GraftM docker image is to  move all the files GraftM needs to access to the current working directory, and use the following command:

```
docker run -v `pwd`:/data graftm_x.x.x-docker_img graft <options>
```

**The harder way** - If you wish to specify a reads file or gpkg that is **not** in the current working directory you will need to mount the path to each file to the image using the -v command as done above, **and** specify the local directory for the file to the GraftM command. For example if I wanted to use a gpkg not in the current directory:

```
docker run -v `pwd`:/data -v /path/to/my_gpkg.gpkg:/gpkg graftm_x.x.x-docker_img graft --forward <my_reads.fa> --graftm_package /gpkg/<my_gpkg.gpkg>
```

We recommend the easier way.
If you still wish to run using files not in the current working directory, please mount each type of data to the correct directory within the image:
* GraftM packages (gpkg) --> **gpkg** (e.g. ```-v /path/to/gpkg:/gpkg```)
* Sequence data --> **reads** (e.g. ```-v /path/to/reads:/reads```)
* Specific search HMM  --> **hmm** (e.g. ```-v /path/to/hmm:/hmm```)

This image is quite large, due to the number of dependencies required to run GraftM - apologies for that. Please do drop a message here on the GitHub page if you have any questions or concerns.
