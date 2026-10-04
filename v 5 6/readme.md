# System Design Primer: Videos 5 to 6 (Pseudocode)

> Playlist: System Design Primer Course
> Notes ki language: Hinglish (Roman script)
> Tag guide: `Extra` = jo video mein nahi tha, revision ke liye add kiya hai
> `⚠️ Correction` = video mein jo galat ya imprecise bola gaya, uska sahi version
> `🔄 Update` = video purana hai, ab jo latest hai wo yahan likha hai
> `💡 Simple Words` = jo cheez confusing ho sakti hai, usse aasan bhasha mein, video ke apne example se samjhaya hai

## Index (is file ke videos)

| # | Video | Link |
|---|---|---|
| 5 | Data and Data Flow | [Jao](#video-5-data-and-data-flow-pseudocode) |
| 6 | Databases and Their Types | [Jao](#video-6-databases-and-their-types-pseudocode) |

---
---

# Video 5: Data and Data Flow (Pseudocode)

## Table of Contents

1. [Quick Overview](#51-quick-overview)
2. [Data system ke core mein kyun hai?](#52-data-system-ke-core-mein-kyun-hai)
3. [Data ka representation (alag alag layers par)](#53-data-ka-representation-alag-alag-layers-par)
4. [Data Flow](#54-data-flow)
5. [Data kahan se aata hai?](#55-data-kahan-se-aata-hai)
6. [Data ke baare mein kaun se factors dekhne hain?](#56-data-ke-baare-mein-kaun-se-factors-dekhne-hain)
7. [Different systems ke examples](#57-different-systems-ke-examples)
8. [Key Takeaways](#video-5-key-takeaways-quick-revision)
9. [Self-Test Questions](#video-5-self-test-questions)

## 5.1 Quick Overview

**Video ka goal:** System design ke basic component **data** ko samjhana: data kaise represent hota hai, system ke andar kaise flow karta hai, components ke beech kaise exchange hota hai, aur system banate waqt data ke baare mein kaun se factors consider karne chahiye.

## 5.2 Data system ke core mein kyun hai?

**Building analogy:** Hotel, hospital, theater jaisi buildings mein **people core entity** hain. Log andar aate hain, rukte hain, bahar jaate hain. Agar log nahi hain to building ka kya faida? (Storage / warehouse jaisi buildings exception hain, yahan people-centric buildings ki baat ho rahi hai.)

| Building | Computing system |
|---|---|
| People building mein aate hain | Data system mein **enter** hota hai |
| People building mein rehte hain | Data system mein **manipulate / compute** hota hai |
| People bahar jaate hain | Data user ko wapas **serve** hota hai |

Users data ko **create** kar sakte hain, sirf **access** kar sakte hain, ya dono. Example: YouTube mein users video upload (create) bhi karte hain aur dekhte (access) bhi hain.

**Isliye data system design ke core mein hai.**

## 5.3 Data ka representation (alag alag layers par)

Data har layer par alag format mein hota hai:

| Layer | Data kis format mein? |
|---|---|
| User / presentation level | Text, videos, images, notes |
| Application layer | JSON, XML, etc. |
| Database / data store | Data structures: tables, indexes, lists, trees (DB technology par depend) |
| Network layer | **Packets** (ek machine se dusri machine) |
| Hardware level | **0 aur 1** (bits) |

```
 User (text/images/videos)
        |
        v
 Application (JSON / XML)
        |
        v
 Database (tables / indexes / trees)
        |
        v
 Network (packets)   ---->   Hardware (0s and 1s)
```

**Ye kyun important hai?** System design karte waqt kam se kam **application, database aur network** teen layers se deal karna padta hai. Har layer par data ke formats aur properties samajhne padte hain, taaki data ka **exchange aur flow efficient** ho aur storage **secure aur effective** ho.

> `⚠️ Correction` (imprecise) Video mein pehli layer ko "business layer or as a user" bola gaya. User jo text, images, videos dekhta hai wo **presentation layer** hai. **Business layer** (business logic) application layer mein aati hai, jahan data JSON/XML jaise formats mein process hota hai.

> `Extra` **Data formats ka comparison:**
>
> | Format | Kahan use hota hai | Note |
> |---|---|---|
> | JSON | Web / REST APIs | Human-readable, sabse common |
> | XML | Purane enterprise systems, SOAP | Verbose, naye APIs mein kam |
> | Protocol Buffers (Protobuf), Avro | gRPC, internal services, event streams | Binary, compact, fast |

> `🔄 Update` Naye systems mein APIs ke liye **JSON** dominant hai aur XML kam use hota hai. Service-to-service communication mein **Protobuf (gRPC)** aur event streaming mein **Avro/Protobuf** common ho gaye hain.

## 5.4 Data Flow

> **Industry ka famous saying:** "Always think about data flow." Jab aap samajh lo ki kis type ka data hai, kis format mein store aur operate karna hai, aur wo application mein kaise flow karega, to design ka aadha safar poora ho jata hai.

### Data stores

Examples: **databases, queues, caches, indexes**.

| Store | Kyun data store hai? |
|---|---|
| Database | Data persist karta hai |
| Queue | Isme bhi data kisi format mein rehta hai (messages) |
| Cache | Data easily retrievable hota hai, database query se bachata hai |
| Index | Data aise store hota hai ki **fast search** ho sake |

### Data kaise flow karta hai?

```
 Application ---> Database ---> Cache ---> Application
 Application ---> Queue ---> Database
```

### Flow ke mechanisms

**APIs, messages, events** ke through data stores aur application ke beech exchange hota hai.

**Decision kaise lete hain?** Kab data DB mein rakhna hai, kab queue chahiye, kab cache chahiye, aur kaun sa method (API / message / event) use karna hai, ye **data ke kind aur system ki requirements** par depend karta hai.

> `Extra` **Synchronous vs Asynchronous flow:**
>
> | | Synchronous (API call) | Asynchronous (message / event) |
> |---|---|---|
> | Kaise | Request bhejo, response ka wait karo | Message queue / event stream mein daalo, baad mein process |
> | Example | App -> API -> DB, turant response | Order place hua -> queue -> email / invoice baad mein |
> | Kab | Turant result chahiye | Kaam heavy ya delay chalta hai, systems decouple karne hain |

> `Extra` Message queues / event streaming ke popular tools: **Kafka, RabbitMQ, Amazon SQS**. Detail aage ke videos mein.

## 5.5 Data kahan se aata hai?

| Source | Matlab | Examples |
|---|---|---|
| **Users** | User system se interact karke data create karta hai | Notes app, calendar app, e-commerce mein order requirements |
| **Internal data** | System khud generate karta hai: **data about data** (metadata), application **logs** | Logs, system metadata |
| **Insights / derived data** | User ke actions se generate hota hai | Invoice (e-commerce), watch history, profile history, payment aur subscription details (YouTube / Netflix) |

## 5.6 Data ke baare mein kaun se factors dekhne hain?

Design se pehle ye factors consider karne zaroori hain:

| Factor | Kyun matter karta hai | Example |
|---|---|---|
| **Type of data** | Text, images, videos: database ka choice badal jata hai | Video storage vs text configurations ke liye alag DB |
| **Volume** | Terabytes vs gigabytes ka system bilkul alag hota hai | TBs of data support karna vs few GBs |
| **Reads aur writes** | Kitna data likha ja raha hai aur kitna padha ja raha hai | Heavy writes + heavy reads, heavy writes + kam reads, kam writes + heavy reads |
| **Security** | Kuch systems mein security sabse upar hai | Banking: request fail ho jaye to chalega, data leak nahi hona chahiye |

Volume aur reads/writes decide karte hain ki **kaun sa data store** aur **kaun si storage strategy** choose karni hai.

> `Extra` **Reads vs Writes ka quick table:**
>
> | Workload | Example | Aam taur par sochne ki direction |
> |---|---|---|
> | Read-heavy | Product catalog, news feed | Caching, read replicas |
> | Write-heavy | Logs, IoT sensor data, event tracking | Write-optimized stores, queues |
> | Dono heavy | Social media, streaming | Scaling + caching + partitioning |

> `Extra` Banking ke example mein jo trade-off dikhta hai (available na ho to chalega, lekin data galat / leak nahi hona chahiye) wo **consistency vs availability** ka trade-off hai (CAP theorem se juda), aage ke videos mein aayega.

## 5.7 Different systems ke examples

| System | Data volume | Mukhya requirement | Kyun |
|---|---|---|---|
| **Authorization system** | Kam (user details, credentials) | **Security aur privacy** bahut high | Credentials safe rahein, galat access na mile |
| **Streaming system** | **High** | Data volume + **retrieval speed** dono high | Bahut saare log ek saath videos dekh rahe hote hain |
| **Transactional system** (banking, e-commerce) | Medium | **Transaction fail na ho, do baar na ho, paisa intact rahe** | Galat order ya order na milna; data ka journey / flow important |
| **Heavy compute system** (ML / AI, camera video processing, GPUs) | Bahut high | Upload + compute zyada, **retrieval kam** | Database aur storage requirements alag hoti hain |

Ye factors aur different data stores ka knowledge aapko aise systems ke liye sahi decisions lene mein madad karta hai.

## Video 5: Key Takeaways (Quick Revision)

1. Building mein **people** core hain, system mein **data** core hai.
2. Data har layer par alag format mein hota hai: user (text/images/videos), application (JSON/XML), DB (tables/indexes/trees), network (packets), hardware (0/1).
3. Design karte waqt kam se kam **application, database, network** layers ke formats samajhne zaroori hain.
4. **"Always think about data flow"**: data type, format aur flow samajh liya to design ka aadha kaam ho gaya.
5. Data stores: **databases, queues, caches, indexes**.
6. Data flow ke mechanisms: **APIs, messages, events**.
7. Data **users** se, **system khud** (logs, metadata) se, aur **insights** (invoice, history) se aata hai.
8. Data ke 4 factors: **type, volume, reads/writes, security**.
9. Authorization = security high, streaming = volume + retrieval high, transactional = correctness, heavy compute = upload/compute high.
10. Banking jaise systems mein "request fail" chalega par "data leak" nahi.

## Video 5: Self-Test Questions

1. Building analogy se samjhao ki data system ke core mein kyun hai.
2. Data ko 5 layers par kaise represent kiya jata hai? Har layer ka format batao.
3. Presentation layer aur business layer mein kya fark hai? (`⚠️ Correction`)
4. "Always think about data flow" ka kya matlab hai?
5. Queue, cache aur index ko data store kyun maana jata hai?
6. APIs, messages aur events mein se choose karne ka decision kis par depend karta hai?
7. Data ke 3 sources batao, har ek ka example do.
8. Data ke 4 factors kaun se hain jo design se pehle dekhne hain?
9. Authorization system aur streaming system ki data requirements mein kya fark hai?
10. Synchronous aur asynchronous data flow mein kya difference hai? (`Extra`)

---
---

# Video 6: Databases and Their Types (Pseudocode)

## Table of Contents

1. [Quick Overview](#61-quick-overview)
2. [Building analogy](#62-building-analogy)
3. [Databases ke types](#63-databases-ke-types)
4. [Relational Databases](#64-relational-databases)
5. [Non-Relational (NoSQL) Databases](#65-non-relational-nosql-databases)
6. [Sab types ka comparison](#66-sab-types-ka-comparison)
7. [Database kaise choose karein?](#67-database-kaise-choose-karein)
8. [Key Takeaways](#video-6-key-takeaways-quick-revision)
9. [Self-Test Questions](#video-6-self-test-questions)
10. [Sources](#video-6-sources)

## 6.1 Quick Overview

**Video ka goal:** Different types ke databases, unke use cases, examples, aur pros / cons samjhana. Focus **relational** aur **non-relational** DBs par hai.

## 6.2 Building analogy

Pichle video mein people = data. To **database = building ke andar ke spaces**, jo people ko house karte hain:

| Building space | Database analogy |
|---|---|
| Hospital ke rooms vs hotel ke rooms | Alag data properties ke liye alag structure |
| Movie theater (screen ke saamne chairs) | Ek specific access pattern ke liye optimized |
| Mall (bade open spaces) | Flexible, free movement |

Data ki **property, volume aur querying requirements** ke hisaab se alag databases alag features aur storage ka tareeka dete hain.

## 6.3 Databases ke types

```
                       Databases
                           |
        +------------+-----+------+-------------+
        |            |            |             |
   Relational   Non-relational  File-type   Network DBs  ...
                 (NoSQL)           DBs
                    |
     +--------+-----+-------+----------+
     |        |             |          |
 Key-value  Column-based  Document   Search
  stores       DBs         DBs         DBs
```

Is video mein focus: **relational** aur **non-relational** (key-value, document, column, search).

## 6.4 Relational Databases

Sabse popular type. Select karne ke **2 factors**: **Schema** aur **ACID properties**.

### 1) Schema

Schema = data **kaise structured** hoga. Relational DB mein **tables aur rows** hote hain.

**Classic example: Employees data**

```
 employees                         department              account
 +----------------------+         +-----------------+     +----------------+
 | id (PK)              |         | id (PK)         |     | id (PK)        |
 | name                 |         | name            |     | balance        |
 | age                  |         | started_on      |     | ...            |
 | phone                |         | ...             |     +----------------+
 | city                 |         +-----------------+            ^
 | department_id (FK) --+-----------------^                      |
 | account_id (FK) -----+------------------------------------------+
 +----------------------+
```

| Term | Matlab |
|---|---|
| **Primary key (id)** | Har employee ko unique identify karta hai |
| **Foreign key** | Dusri table ki row ko refer karta hai (department_id, account_id) |
| **Schema constraint** | Rule: ek employee ko department aur account **hona hi chahiye**, ye values **NULL nahi** ho sakti |

**Kab relational choose karein?** Jab data tables mein represent ho sake aur aapko pata ho ki structure aisa hi rahega.

**Benefits:**
1. **Complex data** ko relational tables mein aasani se represent kar sakte hain.
2. **Schema constraints** se garbage / null / inconsistent data DB mein nahi aata.

### 2) ACID Properties

Pehle ek cheez: **Transaction** = ek aisa kaam jisme ek se zyada steps hote hain, lekin wo **ek poore unit** ki tarah hone chahiye. Jaise paise transfer karna.

| Letter | Property | Matlab (ek line) |
|---|---|---|
| **A** | **Atomicity** | Transaction **ya poori hoti hai ya bilkul nahi** |
| **C** | **Consistency** | DB ke **rules kabhi nahi tootne chahiye** |
| **I** | **Isolation** | Ek saath chalte kaam ek dusre mein **beech mein dakhal na dein** |
| **D** | **Durability** | Ek baar ho gaya to **permanent**, crash ke baad bhi safe |

> `💡 Simple Words` **ACID ek hi example se: Rahul, Priya ko ₹100 bhejta hai**
>
> **Setup:** Rahul ke account mein ₹500, Priya ke account mein ₹300. Total = ₹800.
> Ye ek **transaction** hai jisme 2 steps hain: (1) Rahul ke account se ₹100 kato, (2) Priya ke account mein ₹100 jodo.
>
> | Moment | Rahul | Priya | Total |
> |---|---|---|---|
> | Shuru | 500 | 300 | 800 |
> | Step 1 ke baad (beech ka state) | 400 | 300 | 700 (paisa gayab dikh raha!) |
> | Step 2 ke baad | 400 | 400 | 800 |
>
> **A, Atomicity = "ya poora, ya bilkul nahi"**
> - Maan lo Step 1 hua aur Step 2 se **pehle server crash** ho gaya. Rahul ke ₹100 kat gaye, Priya ko mile nahi. Paisa gayab!
> - Atomicity ka matlab: DB aisa hone hi nahi deta. Ya to **dono steps hote hain**, ya **dono cancel** (Rahul ka ₹100 wapas, jaise kuch hua hi nahi).
> - Analogy: ATM se ya to cash niklega aur balance katega, ya kuch bhi nahi.
>
> **C, Consistency = "rules kabhi na tootein"**
> - DB ke kuch rules hote hain: balance negative nahi ho sakta, aur transfer mein total paisa same rehta hai (₹800 hi).
> - Agar Rahul ke paas sirf ₹50 hote aur wo ₹100 bhejta, to DB transaction **reject** kar deta, kyunki rule "balance 0 se kam nahi" tootta.
> - Matlab: transaction se pehle DB "valid" tha, baad mein bhi "valid" hi rahega.
> - Video ne ise "do logon ko alag value nahi milni chahiye" se samjhaya, jo asal mein isolation / replica-consistency ke zyada kareeb hai (neeche Correction dekho). **Interview ke liye: C = rules na tootein.**
>
> **I, Isolation = "ek ke kaam mein dusra beech mein na ghuse"**
> - Video ka example: balance ₹500 hai. Ek request balance **padh** rahi hai aur usi waqt dusri request use ₹600 **likh** rahi hai.
> - Agar read **write se pehle** hua to 500 dikhega, **baad mein** hua to 600. Read ko kabhi **aadha-adhura (beech ka) state** nahi dikhna chahiye.
> - Matlab: kaam ek saath chal rahe hon tab bhi result aisa ho jaise **ek ke baad ek** hue hon.
> - Analogy: bank counter par jab tak ek customer ka kaam poora nahi hota, dusra beech mein se register nahi uthata.
>
> **D, Durability = "ho gaya to permanent"**
> - Jab DB bol de "transaction successful", uske baad bijli chali jaye ya server restart ho, data **disk par safe** hai.
> - DB pehle sab kuch ek **log** mein likh leta hai, isliye crash ke baad bhi recover kar sakta hai.
> - Analogy: bank ki receipt mil gayi = ab record permanent hai.
>
> **Yaad rakhne ka trick:**
>
> | Letter | Ek line |
> |---|---|
> | A | Ya poora, ya kuch nahi |
> | C | Rules na tootein |
> | I | Beech mein dakhal nahi |
> | D | Permanent save |
>
> **Banking mein ACID kyun zaroori?** Kyunki paisa kabhi gayab, double ya galat nahi hona chahiye. Isi liye banking jaise systems mein relational DB (ACID) choose hota hai.

**Kab relational choose karein (ACID ke liye)?** Jab **transactions** chahiye (banking app) aur **schema fixed** hai jo future mein zyada nahi badlega.

> `⚠️ Correction` (imprecise) Video mein **Consistency** ko "do reads ko alag value nahi milni chahiye" se explain kiya gaya. ACID ka **C** actually ye hai ki har transaction DB ko **ek valid state se dusre valid state** mein le jaye (saare constraints / rules follow ho). "Sabko same value milna" replicas ke beech wali consistency (CAP / linearizability) aur **isolation** se zyada juda hai.

> `⚠️ Correction` (imprecise) Isolation ka matlab "transactions ek dusre ko jaante hi nahi" simplified hai. Actual mein **isolation levels** hote hain (Read Committed, Repeatable Read, Serializable), aur jitna strong level, utna kam anomalies lekin utni kam concurrency. (Ye thoda advanced hai, pehli padhai mein skip kar sakte ho.)

### Relational DBs ki limitations

| Limitation | Detail |
|---|---|
| **Schema evolve karna mushkil** | Jab schema fixed nahi hota aur product ke saath fields badalte hain, to kaam mushkil hota hai. Table bahut badi ho jaye to **naye columns add karna** aur complex hota hai |
| **Joins expensive** | Data bada hone par aur query mein multiple tables se properties fetch karne par **joins costly** ho jate hain, performance expected se kam |
| **Horizontal scaling mushkil** | **Vertical scaling** aasan hai (ek machine ki memory / storage badhao), lekin ek table ko do machines par todna mushkil hai. Application code se kar sakte hain, par difficult hai |

**Vertical scaling:** ek hi machine ko bada karna. **Horizontal scaling:** data / load ko multiple machines mein baantna. (Alag videos mein detail.)

> `🔄 Update` "Relational DBs horizontally scale nahi hote" ab purana claim hai. Aajkal options hain: **read replicas**, **sharding tools** (jaise **Vitess** for MySQL, **Citus** for PostgreSQL), aur **distributed SQL** databases (jaise **Google Spanner, CockroachDB, YugabyteDB, TiDB**) jo SQL + ACID dete hain aur multiple nodes par scale hote hain. Ye "NewSQL" bhi kehlate hain.

> `🔄 Update` Modern relational DBs (jaise **PostgreSQL ka JSONB**, MySQL ka JSON type) mein **semi-structured / flexible data** bhi store ho sakta hai, isliye "flexible schema = sirf NoSQL" ab strict rule nahi.

> `Extra` Popular relational DBs: **MySQL, PostgreSQL, Oracle, SQL Server, SQLite**. Language: **SQL**.

## 6.5 Non-Relational (NoSQL) Databases

Inme schema **fixed nahi** hota, aur alag types alag requirements ke liye bane hain.

### 1) Key-Value Stores

- **Hash map** jaisa: bas ek **key** aur ek **value**.
- **Use cases:** feature flags, discounts / promotions, kisi city mein kisi feature ko enable karna, application / configuration data, request-response store karna, **caching solutions**.
- **Examples:** **Redis, DynamoDB, Memcached**.
- **Benefit:** bahut **fast**, quick access.

```
 key                      value
 ---------------------    --------------------
 feature:dark_mode        true
 promo:diwali             {"discount": 20}
 city:pune:new_feature    enabled
```

> `⚠️ Correction` Video mein bola gaya "zyadatar key-value stores in-memory hote hain". Ye **Redis** aur **Memcached** ke liye sach hai, lekin **DynamoDB** primarily SSD-backed, durable, fully managed database hai (in-memory cache nahi, uska alag caching layer DAX hota hai). Aur DynamoDB **ACID transactions** bhi support karta hai.

> `🔄 Update` **Redis ka licensing badla hai:** 2024 mein Redis ne apna license open-source BSD se hata kar source-available (RSALv2 / SSPL) kar diya tha, jiske baad community ne **Valkey** (Linux Foundation fork) banaya. **Redis 8 (May 2025)** ke saath Redis ne **AGPLv3** option wapas add kar diya. Production choose karte waqt apne license requirement ke hisaab se Redis ya Valkey check karo.

### 2) Document-Based Databases

- **Schema fixed nahi**, jab aapko pata nahi ki fields time ke saath kaise evolve karenge.
- **Heavy reads aur writes** support karte hain.
- Relational ke saath mapping:

| Relational | Document DB |
|---|---|
| Table | **Collection** |
| Row | **Document** |

**Use case:** E-commerce product details (item name, id, price, availability, tax, etc.). Details known hain lekin time ke saath badal sakti hain, aur query mein ye saari properties ek saath chahiye, alag tables mein baantkar joins nahi karne.

### Relational vs Document: ek aur example (user data)

**Relational:** user table (user_id, name, city, country, company) + city table + country table + company table. Poori detail ke liye **4 tables ko query / join** karna padega, aur large user data save karna complicated.

**Document DB:** sab kuch ek hi document mein:

```json
{
  "user_id": 101,
  "name": "Asha",
  "city": "Pune",
  "country": "India",
  "company": "Acme"
}
```

Bas **ek document fetch** karna hai.

### Document DBs ke Cons

| Con | Detail |
|---|---|
| **Schema nahi** | DB mein null / empty values aa sakte hain, application code mein handle karna padta hai |
| **ACID transactions (video ke hisaab se) nahi** | Updates complex ho sakte hain, transaction complete hua ya nahi ye ensure karna application code ka kaam bana |

### Document DBs ke Benefits (summary)

- **Highly scalable**, **sharding** capabilities
- Dynamic data ke liye **schema-less flexibility**
- Special querying, jaise **aggregation queries**
- Examples: **MongoDB** (aur CouchDB, Firestore)

> `⚠️ Correction` + `🔄 Update` Video ka "document DBs ACID transactions nahi dete" ab sahi nahi hai. **MongoDB ne version 4.0 (2018) mein multi-document ACID transactions** add kiye, aur baad mein inhe **sharded clusters** tak extend kiya. Haan, transactions ka performance cost hota hai, aur design aisa rakho ki zyadatar operations ek document ke andar ho jayein (yehi document model ka asli faida hai).

### 3) Column-Based DBs (Wide-Column Stores)

- Relational aur document ke **beech ka rasta**: ek tarah ka **fixed schema** (tables aur columns) hota hai, lekin **ACID transactions** classic roop mein nahi hote.
- **Use cases:** **event data / streaming data**. Example: music app mein song like, skip, favorite karna, ye saari interactions DB mein event data ki tarah likhi jati hain taaki analytics chalayi ja sake. Aur: health tracking data, **IoT sensors** ka data (har 10 / 30 seconds mein).
- Table structure **queries ke hisaab se** design hota hai (query-first design).
- **Distributed databases** ke liye acche hain.
- **Examples:** **Cassandra, HBase, ScyllaDB**.

**Music app ka example (query-first tables):**

| Table | Kaam |
|---|---|
| `users` | User details |
| `songs` | Song details |
| `users_by_liked_song` | Kisi song ko kin users ne like kiya |
| `songs_liked_by_user` | Kisi user ne kaunse songs like kiye |

Har query pattern ke liye alag table, isliye reads fast rehte hain.

> `⚠️ Correction` Video mein column DBs ko pehle "heavy reads" ke liye bola gaya, phir kaha ki ye "large number of heavy **writes**" support karte hain aur "huge number of reads" nahi, ye contradiction hai (transcript mein "writes" ke jagah "rides" aur "reads" ke jagah "leads" garbled aaya). Sahi picture: column / wide-column DBs (jaise Cassandra) **write-heavy** workloads ke liye bane hain aur reads **pehle se decide kiye gaye query patterns** par fast hote hain, arbitrary ad-hoc queries (aur joins) par nahi.

> `🔄 Update` Cassandra mein **lightweight transactions (LWT)** pehle se hain (single-partition conditional updates). Ab **Accord** naam ka leaderless consensus protocol Cassandra mein **multi-partition ACID transactions** (strict serializable isolation) la raha hai. Ek June 2026 ke article ke hisaab se **Cassandra 6.0 us waqt alpha stage mein tha**, isliye production use se pehle latest release status check karo.

### 4) Search Databases

- **Full-text search** queries ke liye: flight / movie booking, Amazon par item search.
- **Analogy (book index):** Kitab ke shuru mein index hota hai ("Chapter 5 -> page 237"). Waise hi search DBs mein data **advanced indexes** mein store hota hai taaki search queries ka jawab fast mile (jaise "post it" search karna).
- **Examples:** **Elasticsearch, Apache Solr**.
- **Important:** Search DB **primary data store nahi** hota. E-commerce mein product catalog primary DB (relational ya non-relational) mein hota hai, aur frequently queried / search ka data search DB mein store aur refresh hota hai.

> `Extra` Search DBs andar se **inverted index** use karte hain (word -> kaun se documents mein hai), isiliye full-text search fast hoti hai. Underlying library aam taur par **Apache Lucene** hai.

> `🔄 Update` Elasticsearch ke licensing mein bhi badlav hue hain, aur AWS ne uska fork **OpenSearch** banaya hai. Naye project mein dono options dekho aur latest licence terms check karo.

### 5) Baaki use cases (video ne briefly mention kiye)

| Data type | Kahan store karte hain |
|---|---|
| **Images aur videos** | Cloud **object storage**: Amazon S3 ya GCP ke buckets (Google Cloud Storage) |
| **Large datasets / time-series data** (analytics) | Specialized databases (details video ki description mein) |

> `Extra` **Object storage** (S3, GCS, Azure Blob) mein files "objects" ki tarah rakhi jati hain aur DB mein sirf unka URL / metadata rakhte hain. Time-series DBs: **InfluxDB, TimescaleDB, Prometheus**. Graph DBs (relationships ke liye): **Neo4j**.

> `🔄 Update` **Vector databases** ab ek common naya type hai (embeddings, semantic search, RAG ke liye): jaise **Pinecone, Milvus, Qdrant, pgvector** (PostgreSQL extension), aur kai existing DBs (Redis, Elasticsearch, MongoDB) mein bhi vector search aa gaya hai. Ye video ke time par itna common nahi tha.

## 6.6 Sab types ka comparison

| Type | Data model | Examples | Best use cases | Pros | Cons |
|---|---|---|---|---|---|
| **Relational** | Tables, rows, fixed schema | MySQL, PostgreSQL | Transactions, structured data, relations (banking, employees) | ACID, constraints, complex data, joins | Schema change aur joins at scale mushkil, horizontal scaling mushkil (classic) |
| **Key-value** | Key -> value | Redis, DynamoDB, Memcached | Cache, feature flags, config, sessions | Bahut fast | Limited querying |
| **Document** | Collections, documents, flexible schema | MongoDB | Product catalog, user profiles, evolving schema, heavy reads / writes | Flexible, scalable, sharding, aggregation | Schema nahi (nulls), transactions ka cost / limits |
| **Column (wide-column)** | Query-first tables | Cassandra, HBase, ScyllaDB | Event data, IoT, write-heavy, distributed | Bahut scalable, distributed | Limited query flexibility, joins nahi |
| **Search** | Inverted indexes | Elasticsearch, Solr | Full-text search | Fast search | Primary store nahi |
| **Object storage** | Blobs / files | S3, GCS | Images, videos | Cheap, scalable | Queryable nahi |

## 6.7 Database kaise choose karein?

- Ye sab **thumb rules** hain, **strict rules nahi**.
- Kuch cases mein aasan hai (e.g. config / flags -> key-value store).
- Jab requirements **fuzzy** hon aur data kaise evolve hoga ye pata na ho, to relational vs non-relational ya document vs column ka decision mushkil hota hai. Tab **team ke saath baithkar pros / cons weigh** karte hain.
- Ho sakta hai product ke shuru mein relational DB choose kiya ho, aur **5-10 saal baad**, jab scale aur data growth bahut ho jaye, **doosre database par migrate** karna pade.
- Bade companies kabhi kabhi **apne in-house database solutions** bhi banati hain.
- **Koi right ya wrong answer nahi hai.**

> `Extra` **Polyglot persistence:** real systems mein aksar **ek se zyada databases** saath mein use hote hain. Example: e-commerce mein primary data relational DB mein, cache Redis mein, search Elasticsearch mein, images S3 mein.

> `Extra` **ACID vs BASE:** Kai NoSQL DBs **BASE** (Basically Available, Soft state, Eventual consistency) model par chalte hain, yaani strong consistency ki jagah availability aur scale ko prefer karte hain. Ye CAP theorem wale video mein detail se aayega.

> `Extra` Video ke end mein bola gaya ki aage replication, indexing, sharding, scaling ke videos aayenge.

## Video 6: Key Takeaways (Quick Revision)

1. **Relational DB** choose karo jab **fixed schema**, **complex relations** aur **ACID transactions** chahiye (banking).
2. Relational ke fayde: complex data represent karna aur **constraints** se bad data rokna.
3. **ACID** = Atomicity (all or nothing), Consistency (valid state), Isolation (concurrent transactions alag), Durability (disk par persist).
4. Relational ki limits: schema evolve mushkil, **joins** costly, **horizontal scaling** mushkil (classic), lekin distributed SQL ab options deta hai.
5. **Key-value:** hash map jaisa, bahut fast, cache / flags / config (Redis, DynamoDB, Memcached).
6. **Document:** flexible schema, heavy reads / writes, ek hi document mein related data (MongoDB). MongoDB multi-document ACID transactions bhi support karta hai.
7. **Column / wide-column:** write-heavy, event / IoT data, query-first design (Cassandra, HBase, ScyllaDB).
8. **Search DB:** full-text search ke liye indexes (Elasticsearch, Solr), **primary store nahi**.
9. Images / videos **object storage** (S3 / GCS) mein, large analytics / time-series ke liye specialized DBs.
10. DB choice **thumb rules** se hota hai, strict rules se nahi, aur real systems mein aksar **multiple DBs** saath chalte hain.

## Video 6: Self-Test Questions

1. Building analogy se databases ko samjhao.
2. Relational DB select karne ke 2 factors kaun se hain?
3. Primary key aur foreign key kya hote hain? Employee table ka example do.
4. ACID ke 4 letters ka matlab batao, har ek ka ek example do.
5. ACID mein "Consistency" ka sahi matlab kya hai? (`⚠️ Correction`)
6. Relational DBs ki 3 limitations kaun si hain? Aajkal inhe kaise address kiya ja raha hai? (`🔄 Update`)
7. Key-value store kab use karoge? DynamoDB in-memory hota hai ya nahi? (`⚠️ Correction`)
8. Document DB aur relational DB mein user data store karne ka fark samjhao. Document DB ke 2 cons batao.
9. Column DBs kis type ke workload ke liye bane hain? Music app ke liye query-first tables ka example do.
10. Search DB primary data store kyun nahi hota? Ek e-commerce system mein kaun sa data kahan store karoge? (`Extra`: polyglot persistence)

## Video 6: Sources

- [Redis reverts to open source with AGPL (InfoQ)](https://www.infoq.com/news/2025/05/redis-agpl-license)
- [Open source wins again! Redis adds GNU AGPL license (SD Times)](https://sdtimes.com/os/open-source-wins-again-redis-adds-gnu-agpl-license-to-its-offering/)
- [Apache Cassandra 6.0: Accord ACID transactions and release status (The New Stack)](https://thenewstack.io/apache-cassandra-6-features/)
- [Cassandra to get ACID transactions via Accord consensus protocol (BigDATAwire)](https://bigdatawire.com/2022/10/14/cassandra-to-get-acid-transactions-via-new-accord-consensus-protocol)
- [MongoDB multi-document ACID transactions general availability (MongoDB blog)](https://www.mongodb.com/blog/post/mongodb-multi-document-acid-transactions-general-availability)
- [ACID transactions with MongoDB](https://mongodb.com/transactions)