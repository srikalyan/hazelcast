

### Sample JBoss Web Application Configuration

- Place the `hazelcast-`*version*`.jar` into `JBOSS_HOME/server/deploy/default/lib` directory.
- Place the `hazelcast-ra-`*version*`.rar` into `JBOSS_HOME/server/deploy/default/deploy` directory
- Create a `hazelcast-ds.xml` file at `JBOSS_HOME/server/deploy/default/deploy` directory containing below content. Make sure to set the `rar-name` element to `hazelcast-ra-`*version*`.rar`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE connection-factories
  PUBLIC "-//JBoss//DTD JBOSS JCA Config 1.5//EN"
  "http://www.jboss.org/j2ee/dtd/jboss-ds_1_5.dtd">

<connection-factories>
 <tx-connection-factory>
      <local-transaction/>
      <track-connection-by-tx>true</track-connection-by-tx>
      <jndi-name>HazelcastCF</jndi-name>
      <rar-name>hazelcast-ra-<version>.rar</rar-name>
      <connection-definition>
           javax.resource.cci.ConnectionFactory
      </connection-definition>
  </tx-connection-factory>
</connection-factories>
```

- Add the following lines to the `web.xml` file.

```xml
<resource-ref>
    <res-ref-name>HazelcastCF</res-ref-name>
    <res-type>com.hazelcast.jca.ConnectionFactoryImpl</res-type>
    <res-auth>Container</res-auth>
</resource-ref>
```

- Add the following lines to the `jboss-web.xml` file.

```xml
<resource-ref>
    <res-ref-name>HazelcastCF</res-ref-name>
    <jndi-name>java:HazelcastCF</jndi-name>
</resource-ref>
```

If Hazelcast resource is used from EJBs, you should configure `ejb-jar.xml` and `jboss.xml` for resource reference and JNDI definitions.

<br> </br>


