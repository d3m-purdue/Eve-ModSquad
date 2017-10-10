# ta23-purdue-cra
TA2/TA3 integration between Purdue and Charles River Analytics teams

## Setup Instructions

1. Pull down the latest Eve TA2 Docker image: `docker pull
   registry.datadrivendiscovery.org/eve/docker-images`.

2. Clone the Modsquad TA3 repository: `git clone
   https://github.com/d3m-purdue/modsquad -b ta23-cra`.

3. Follow the build instructions at
   https://github.com/d3m-purdue/modsquad/README.md.

4. Download the seed dataset: `curl -O
   https://datadrivendiscovery.org/data/seed_datasets/o_185.tar.gz && gunzip
o_185.tar.gz`.  You may need to do this step through a web browser to handle D3M
credentials.

5. Copy the seed dataset into a shared directory for TA2 and TA3: `mkdir
   /storage/datasets/seed && cp -rv o_185 /storage/datasets/seed`.

6. Copy the config file into the shared directory: `cp config.json /storage`.

7. Launch the TA2 Docker container: `docker run -e
   CONFIG_JSON_PATH=/storage/config.json -v /storage:/storage -p 50001:50061 -it
--entrypoint /bin/bash register.datadrivendiscovery.org/eve/docker-images -c
"/app/bin/eve grpc-server"`.

8. Launch the TA3 server: `cd modsquad && PORT=8080
   CONFIG_JSON_PATH=/storage/config.json npm run serve`.

9. Visit http://localhost:8080 to try out the integration.
