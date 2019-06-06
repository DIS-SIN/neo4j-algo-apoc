# Neo4j docker

## The empowered version of Neo4j with apoc and algo libraries

### A. (Optional) Configure access to local directory using `set_env.sh`. 

        source ./set_env.sh

What does it configure:

- NEO4J_DIR: by default the current directory and all other are configured by default as its subdirectories

        export NEO4J_DIR=$PWD

- NEO4J_DIR_CONF (optional): use this only if you need a custom `neo4j.conf`

        export NEO4J_DIR_CONF=$NEO4J_DIR/conf

- NEO4J_DIR_DATA: this is where the physical storage for the neo4j instance

        export NEO4J_DIR_DATA=$NEO4J_DIR/data

- NEO4J_DIR_LOGS: this is to map to the `/logs/` directory of the neo4j instance, useful if you want to monitor neo4j log, especially the `debug.log`

        export NEO4J_DIR_LOGS=$NEO4J_DIR/logs

- NEO4J_DIR_IMPT: configure this - and likely you need - a place where from additional data can be imported into the neo4j instance

        export NEO4J_DIR_IMPT=$NEO4J_DIR/import
        
### B. Using the docker image `neo4j-3.5.5:algo-apoc`

1. Create a container and run it with `docker-compose`
- create and run the container

        docker-compose up

- set password, type in your browser: `localhost:7474`. default password is `neo4j`

- check if APOC and ALGO libraries are ready by typing in to the neo4j browser:

        RETURN apoc.version();
        RETURN algo.version();

2. Monitoring: open a new terminal

        source ./set_env.sh
        tail -f $NEO4J_DIR_LOGS/debug.log

3. Shutdown the container

        docker-compose down

4. Remove

        docker-compose rm

## Notes:

#### Following configuration options are by default. 
Neo4j 3.5.5 community edition, 2GB for heap size, 2GB for pagecache, all APOC and ALGO functions/procedures are available, import from/export to local physical files are allowed, HTTP connection timeouts (to external servers) are configured, and job thread pool is also configured as below.

- dbms.memory.heap.initial_size=2G
- dbms.memory.heap.max_size=2G
- dbms.memory.pagecache.size=2G
- dbms.security.procedures.unrestricted=apoc.\*,algo.\*
- apoc.export.file.enabled=true
- apoc.import.file.enabled=true
- apoc.http.timeout.connect=60000
- apoc.http.timeout.read=120000
- apoc.jobs.pool.num_threads=4
- apoc.jobs.schedule.num_threads=4
