# Galaxy job\_conf.xml

job.conf.xml file | Description| Issues| Tested with
---|---|---|---|
*docker\_default\_local\_job\_conf.xml* | Configuration to run galaxy jobs using dockerized tools with mulled | The configuration work without any problem. It is also possible to attach CVMFS volumes for reference data. Some tools can't be run with mulled, for this reason it is better to specify the tools that should run with Conda in the tool block. | Galaxy 18.05
*singularity\_job\_conf.xml* | Configuration to run jobs with Singularity containers | It works fine, also with CVMFS volumes (one for singularity images, /cvmfs/singularity.galaxyproject.org, and one for reference data). Required Galaxy version: Galaxy >= 18.09 (the job_conf has the singularity block ``<param id="singularity_image_dir">PATH</param>``). | Galaxy 19.01
*docker\_optional\_job\_conf.xml* | Configuration to run tools that supports Docker container on a specifcic destination, Conda will be the default dependency resolver for the others | Using dynamic runner and docker_dispatch destination xml ``<destination id="docker\_dispatch" runner="dynamic">`` tools that supports Docker container are redirected to a different destination (local_docker). Not working on Galaxy 18.05. | Galaxy 19.05
*chronos\_job\_conf.xml* | Configuration to run galaxy jobs on an Apache MESOS cluster | The jobs run but there are problems linking the results in the history. The runner chronos.py called by the chronos destination block lacks of some features: it is not possible to attach more than one volume (e.g. add CVMFS for reference data), the jobs are not executed in the default working directory and this parameter can not be set, thus resulting in the problem with history results link. | Galaxy 18.05

In all the configuration the upload1 tool is setted to be run in local destination in order to allow the upload of files. 
