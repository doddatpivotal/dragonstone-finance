Test ratings locally
- delete database schemas
- Launch MySql
- Run config server `./gradlew bootRun`
- Run discovery server `./gradlew bootRun`
- Launch ratings API first to create tables
```
SPRING_PROFILES_ACTIVE=local java -jar target/ratings-api-0.0.1-SNAPSHOT.jar
```
- Launch ratings loader to load data (you should see COMPLETED in logs)
```
SPRING_PROFILES_ACTIVE=local java -jar target/ratings-loader-0.0.1-SNAPSHOT.jar localFilePath=classpath:data.csv
```
- access http :8081/ratings and you should have 3 results
```
SPRING_PROFILES_ACTIVE=local java -jar target/trades-loader-0.0.1-SNAPSHOT.jar localFilePath=classpath:data.csv
```



What we have
- Multiple datasources
- 

TODO
- Review all files
- Add the api call

# Note on DB's
- rating table does not grow, so no incrementing apis.  JPA creates table through API launch



cf create-service p-service-registry standard discovery-server 
cf create-service p-config-server standard config-server -c '{"git":{"uri":"https://github.com/doddatpivotal/dragonstone-finance.git","searchPaths":"dragonstone-finance-config","label":"master"}}'
cf create-service nfs Existing volume-service -c '{"share":"nfs-pcf.pez.pivotal.io/pcfone/dpfeffer"}'
cf create-service p.mysql db-small app-db

http https://auditor-api.apps.pcfone.io/trades
http https://ratings-api.apps.pcfone.io/ratings