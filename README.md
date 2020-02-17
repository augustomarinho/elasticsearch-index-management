# Elastic Search Index Management

Check out this project and following thisa above steps:

1. Run the following command: `sudo sysctl -w vm.max_map_count=262144`

2. Run `git clone git@github.com:augustomarinho/springboot-fluentd-appender.git`

3. Run `mvn clean install docker:build`

4. Run `docker run -d --name springboot-app \ --label elastic_index=springboot \ --label send.logs=true \ -p 8002:8080 \ augustomarinho/springboot-fluentd-appender`

5. Edit your Elastic Search IP in [filebeat.yml](configs/filebeat/filebeat.yml)

6. Run `docker run -d \ --name=filebeat \ --user=root \ --volume="$(pwd)/configs/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml:ro" \ --volume="/var/lib/docker/containers:/var/lib/docker/containers:ro" \ --volume="/var/run/docker.sock:/var/run/docker.sock:ro" \ docker.elastic.co/beats/filebeat:7.0.0 filebeat -e -strict.perms=false`

7. Run `docker-compose -f docker-compose-es-kibana.yml -d --force-recreate`

8. Open [Kibana Dev Tools](http://localhost:5601/app/kibana#/dev_tools/console)

9. In Kibana Dev Tools, execute this http command in sequence

10. [create-policy.txt](configs/create-policy.txt)

11. [create-template.txt](configs/create-template.txt)

12. [create-index-app-1.txt](configs/create-index-app-1.txt)

13. [create-alias.txt](configs/create-alias.txt)

From here, It's possible insert documents in created index, running this command: `curl -X GET http://localhost:8002/query/cpf/12345678909 -i`

Execute some time this commnad above to insert more documents in created index.

For you check roll over index working, run the commands below in [Kibana Dev Tools](http://localhost:5601/app/kibana#/dev_tools/console):

1. [check-index-rollover.txt](configs/check-index-rollover.txt)

2. [roll over-index.txt](configs/rollover-index.txt)

3. Write more documents in rolled over index. Run `curl -X GET http://localhost:8002/query/cpf/12345678909 -i`

For testing the index aggregation in the same reading alias, run the commands below in [Kibana Dev Tools](http://localhost:5601/app/kibana#/dev_tools/console)

1.  [check-index-app-2.txt](configs/create-index-app-2.txt)

2.  Edit de timestamp value for curent time, before running [write-idex-app-2.txt](configs/write-idex-app-2.txt)

Following this steps, It's possible test the roll over index using ILM (Index Lifecycle Management) from Elastic Search
