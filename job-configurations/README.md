# Galaxy job\_conf.xml

job.conf.xml file | Description| Issues| Galaxy release
---|---|---|---|
*chronos\_job\_conf.xml* | configuration to run galaxy jobs on an Apache MESOS cluster | The jobs are run but there are problem in linking the results in the history, the runner chronos.py called by the chronos destination block lacks some features: it is not possible to attach more than one volume (e.g. cvmfs for reference data), the jobs are not executed in the default working directory and this parameter can not be set. | Galaxy 18.05
*docker\_default\_local\_job\_conf.xml* | Configuration to run galaxy jobs using tools dockerized with mulled | The configuration work without problems is also possible to attach cvmfs volumes for reference data. Some of the tools can't be run with mulled, for this reason is better to specify the tools that should run with Conda in the tool block. | Galaxy 18.05
*singularity\_job\_conf.xml* | Configuration file to run jobs with  Singularity container | It works fine with attached cvmfs volumes (one for singularity images, /cvmfs/singularity.galaxyproject.org, and one for reference data). Galaxy >= 18.09 (the job_conf has the singularity block ```<param id="singularity_image_dir">PATH</param>```). | Galaxy 19.01
*docker\_optional\_job\_conf.xml* | Configuration to run specific tools on docker destination, Conda will be the default dependency resolver | It works but all Docker tools has to be defined in the ```<tools></tools>``` block. To resolve this problem i tried to use dynamic destination ```xml <destination id="docker\_dispatch" runner="dynamic">``` which is not working on Galaxy 18.05. | Galaxy 18.05

In all the configuration the upload1 tool is setted to be run in local destination in order to allow the upload of files. 
