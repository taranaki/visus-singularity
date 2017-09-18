BootStrap: docker
From: visus/visus:singularity

%runscript
  echo "Arguments: <optional_port> on which to run the server (default: 8080)"
  re='^[0-9]+$'
  PORT=${1:-8080}
  if ! [[ $PORT =~ $re ]]; then
    echo "WARNING: Invalid port specified ($1)"
    echo "         Using default port 8800."
    PORT=8800
  fi
  umask 022
  cd /tmp/apache2
	mv ports.conf ports.conf.orig
  sed 's/80/${PORT}/' ports.conf.orig > ports.conf
	mv sites-enabled/webviewer.conf sites-enabled/webviewer.conf.orig
  sed 's/80/${PORT}/' sites-enabled/webviewer.conf.orig > sites-enabled/webviewer.conf

  echo "Starting visus server"
  echo "Connect to `hostname`:$PORT"
  exec service apache2 start
