
  1) run docker hello-world
      - start
      - see process stats (ps)
      - remove it from stopped instances
   2) whalesay
      - show docker/whalesay history
   3) smart whalesay
      - build Docker Image from Dockerfile
   4) run jupyter locally
      - volumes and persistent data
   5) run RStudio locally
   6) AWS deployment
      - IP: 35.157.121.151
      - Port open to public: 80
      - ssh connection
      - start image
         - docker run -d -p 80:8888 jupyter/minimal-notebook
      - see in browser that it has started

