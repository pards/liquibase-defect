Liquibase Export Defect Demo
============================

This repo contains two modules
- liquibase-export-fatjar
- liquibase-export-lib

# liquibase-export-fatjar

This is a standalone Spring Boot application with Liquibase enabled, with db migration configs and scripts

You can run this from your IDE by running `com.egalitech.liquibase.export.LiquibaseExportApplication`

# liquibase-export-lib

This is a Java library that contains Liquibase migration configs and scripts

Reproducing the Defect
======================

Show that it works for the `lib` project
----------------------------------------

```
mvn clean install
rm -rf liquibase_libs
mkdir -p liquibase_libs
cp liquibase-export-lib/target/liquibase-export-lib-0.0.1-SNAPSHOT.jar liquibase_libs

liquibase --changelog-file liquibase-changelog.yml --defaults-file liquibase.properties --url 'jdbc:h2:mem:lib;MODE=ORACLE' updateSQL
```

You should see a bunch of SQL displayed on the console

Show that it does NOT work for the `fatjar` project
---------------------------------------------------

```
mvn clean install
rm -rf liquibase_libs
mkdir -p liquibase_libs
cp liquibase-export-fatjar/target/liquibase-export-fatjar-0.0.1-SNAPSHOT.jar liquibase_libs

liquibase --changelog-file liquibase-changelog.yml --defaults-file liquibase.properties --url 'jdbc:h2:mem:lib;MODE=ORACLE' updateSQL
```

This results in the error:
```
Unexpected error running Liquibase: liquibase-changelog.yml does not exist
```
