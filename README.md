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

### Mount a different config folder to host other datasets (must contain server.config and .htpasswd)
`singularity run --bind /local/config:/visus/config ./taranaki-visus-singularity-master.img`

### Mount a different cache folder for the visus server [desired, but not working: can't bind /tmp paths]
`singularity run --bind /data/cache:/tmp/visus_cache ./taranaki-visus-singularity-master.img`
