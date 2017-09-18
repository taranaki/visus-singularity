# visus-singularity

### First, pull the singularity image:
`singularity pull shub://taranaki/visus-singularity`

### Basic start on default port 8080
`singularity run ./taranaki-visus-singularity-master.img`

## Using the lightweight web viewer

Simply browse to [http://localhost:8080](http://localhost:8080).

## Interacting with the ViSUS web server

[API Documentation](http://wiki.visus.org/index.php?title=ViSUS_Server#Supported_Requests)

## Customizations

### How to change the port
`singularity run ./taranaki-visus-singularity-master.img 8088`

### Mount a different /tmp folder to avoid conflicts when running multiple instances
```
singularity run --workdir /tmp/singularity.8085 ./taranaki-visus-singularity-master.img 8085
singularity run --workdir /tmp/singularity.8088 ./taranaki-visus-singularity-master.img 8088
```

### Mount a different config folder to host other datasets (must contain server.config and .htpasswd)
`singularity run --bind /local/config:/visus/config ./taranaki-visus-singularity-master.img`

### Mount a different cache folder for the visus server [not working: can't bind /tmp paths]
`singularity run --bind /data/cache:/tmp/visus_cache ./taranaki-visus-singularity-master.img`

### Example of how to change the server configuration
Coming soon...

### Example of how to provide secure access for specific users
Coming soon...
