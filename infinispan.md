## **Infinispan Notes**  

### **What is Infinispan?**  
Infinispan is an open-source, highly scalable, in-memory data grid and caching solution developed by Red Hat. It is designed for high-performance computing, clustering, and distributed caching.  

---

### **Key Features of Infinispan**  

1. **In-Memory Data Grid:**  
   - Stores data in memory, reducing database calls and improving performance.  
   - Supports both local and distributed caching.  

2. **Clustering & Scalability:**  
   - Can be used in a single-node or multi-node cluster.  
   - Supports horizontal scaling by adding more nodes dynamically.  

3. **Distributed & Replicated Cache Modes:**  
   - **Replicated mode:** Each node holds a full copy of the data.  
   - **Distributed mode:** Data is spread across multiple nodes to balance memory and performance.  

4. **Persistence & Store Mechanism:**  
   - Can persist data to external storage (e.g., database, file system).  
   - Supports JDBC, RocksDB, and other persistent storage backends.  

5. **Transactions & Concurrency:**  
   - Provides ACID-compliant transactions.  
   - Supports optimistic and pessimistic locking for concurrent data access.  

6. **Event Listeners & Notifications:**  
   - Supports event-driven programming.  
   - Allows cache entry notifications for changes.  

7. **Querying & Indexing:**  
   - Supports SQL-like queries using **Ickle Query Language**.  
   - Integrates with Hibernate Search for full-text searching.  

8. **Security & Authentication:**  
   - Provides role-based access control.  
   - Supports authentication via OAuth, LDAP, and other security mechanisms.  

9. **Integration with Java & Spring Boot:**  
   - Offers a Java API for direct interaction.  
   - Has Spring Boot integration for caching use cases.  

---

### **Installation & Setup**  

#### **1. Adding Infinispan to a Spring Boot Project**  
Add the following dependency in `pom.xml`:  

```xml
<dependency>
    <groupId>org.infinispan</groupId>
    <artifactId>infinispan-spring-boot-starter-remote</artifactId>
    <version>14.0.0</version>
</dependency>
```

#### **2. Configure `application.properties` for Infinispan Remote Cache**
```properties
infinispan.remote.server-list=127.0.0.1:11222
infinispan.remote.use-auth=true
infinispan.remote.auth-username=admin
infinispan.remote.auth-password=admin123
```

#### **3. Basic Cache Usage in Java**
```java
@Autowired
private RemoteCacheManager cacheManager;

public void putDataInCache() {
    RemoteCache<String, String> cache = cacheManager.getCache("myCache");
    cache.put("key1", "Hello Infinispan!");
    System.out.println("Cached Value: " + cache.get("key1"));
}
```

---

### **Cache Modes in Infinispan**  

| Cache Mode         | Description |
|--------------------|-------------|
| Local Cache       | Data stored in a single node, no replication. |
| Replicated Cache  | Data is copied across all nodes in the cluster. |
| Distributed Cache | Data is split among nodes to balance memory load. |
| Invalidation Mode | Nodes remove entries when data changes elsewhere. |
| Transactional Cache | Supports ACID transactions in a cache. |

---

### **Common Use Cases**  

✅ **High-Performance Caching** – Reduce load on databases.  
✅ **Distributed Session Management** – Share session data across multiple servers.  
✅ **Event-Driven Systems** – Use notifications and listeners.  
✅ **Real-Time Data Processing** – Leverage in-memory computation.  

---

Would you like me to add specific use cases or a hands-on guide for clustering? 🚀
