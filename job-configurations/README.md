# Galaxy job\_conf.xml

job.conf.xml file | Description| Issues| Tested with
---|---|---|---|
*chronos\_job\_conf.xml* | Configuration to run galaxy jobs on an Apache MESOS cluster | The jobs run but there are problems linking the results in the history. The runner chronos.py called by the chronos destination block lacks of some features: it is not possible to attach more than one volume (e.g. add CVMFS for reference data), the jobs are not executed in the default working directory and this parameter can not be set, thus resulting in the problem with history results link. | Galaxy 18.05

*docker\_default\_local\_job\_conf.xml* | Configuration to run galaxy jobs using tools dockerized with mulled | The configuration work without any problem. It is also possible to attach CVMFS volumes for reference data. Some tools can't be run with mulled, for this reason is better to specify the tools that should run with Conda in the tool block. | Galaxy 18.05

*singularity\_job\_conf.xml* | Configuration to run jobs with Singularity container | It works fine, with also CVMFS volumes (one for singularity images, /cvmfs/singularity.galaxyproject.org, and one for reference data). Required Galaxy version: Galaxy >= 18.09 (the job_conf has the singularity block ```<param id="singularity_image_dir">PATH</param>```). | Galaxy 19.01

*docker\_optional\_job\_conf.xml* | Configuration to run specific tools on docker destination, Conda will be the default dependency resolver | It works but all Docker tools has to be defined in the ```<tools></tools>``` block. To solve this problem we tried to use dynamic destination ```xml <destination id="docker\_dispatch" runner="dynamic">``` which is not working on Galaxy 18.05. | Galaxy 18.05

In all the configuration the upload1 tool is setted to be run in local destination in order to allow the upload of files. 
