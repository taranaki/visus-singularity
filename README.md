# visus-singularity

### First, pull the singularity image:
`singularity pull shub://taranaki/visus-singularity`

### Basic start on default port 8080
`singularity run ./taranaki-visus-singularity-master.img`

### How to change the port
`singularity run ./taranaki-visus-singularity-master.img 8088`

### Mount a different /tmp folder to avoid conflicts when running multiple instances
`singularity run --workdir /tmp/singularity.8085 ./taranaki-visus-singularity-master.img 8085`
`singularity run --workdir /tmp/singularity.8088 ./taranaki-visus-singularity-master.img 8088`

### Mount a different config folder to host other datasets
`singularity run --bind /scratch/datasets/local:/home/visus/datasets ./taranaki-visus-singularity-master.img`

### Mount a different cache folder for the visus server
`singularity run --bind /data/cache:/tmp/visus_cache ./taranaki-visus-singularity-master.img`


TODO:
 X recreate docker image
   X envvars might actually be good to go, keep it in /etc/apache2
   X use webviewer.conf instead of 000-default.conf
     X move webviewer.conf to /tmp/apache2/sites-enabled on startup
     X apache2.conf: include /tmp/apache2/sites-enabled/* (which contains webviewer.conf)
     X changed name of viewer to webviewer (update .conf)
   X mount cache to /tmp/visus_cache instead of /home/visus/cache
     X recompile mod_visus to use this path
   X move .htpasswd from apache to config
     X where is this referenced? httpd.conf? webviewer.conf!
   X get rid of /home/visus/apache2 (it will now be /tmp/apache2)
     X make the /tmp/apache2 directory a tgz file which docker will extract (otherwise, the empty directories will not be committed to github and will not be copied and stupid apache won't just create them)
   X use /visus instead of /home/visus (singularity discourages anything in /home)
 - test singularity /tmp with /tmp is remapped (will /tmp/visus_cache get remapped?)
 - remove out-of-date images from dockerhub visus (webviewer, mod_visus, ???)
 - fix the webviewer for the climate demo
   - make it list sub-datasets correctly
   - transfer functions
   - maybe use 3d viewer for 2d data as well instead of OSD
   - host some 3d datasets as well
   - bonus: add some scripting to compare two datasets, compute averages, etc

[ ] First, get the version working without visuspy (docker and singularity)
[ ] Second, get the docker visuspy working
[ ] Third, get the docker mod_visus+visuspy working using multi-stage build (https://docs.docker.com/engine/userguide/eng-image/multistage-build/)
[ ] Finally, get the multistage singularity working (should be just as simple as the original version)
