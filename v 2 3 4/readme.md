# System Design Primer: Videos 2 to 4 (Pseudocode)

> Playlist: System Design Primer Course
> Notes ki language: Hinglish (Roman script)
> Tag guide: `Extra` = jo video mein nahi tha, revision ke liye add kiya hai
> `⚠️ Correction` = video mein jo galat ya imprecise bola gaya, uska sahi version
> `🔄 Update` = video purana hai, ab jo latest hai wo yahan likha hai

## Index (is file ke videos)

| # | Video | Link |
|---|---|---|
| 2 | Components of System Design | [Jao](#video-2-components-of-system-design-pseudocode) |
| 3 | Client-Server Architecture | [Jao](#video-3-client-server-architecture-pseudocode) |
| 4 | Forward and Reverse Proxies | [Jao](#video-4-forward-and-reverse-proxies-pseudocode) |

---
---

# Video 2: Components of System Design (Pseudocode)

## Table of Contents

1. [Quick Overview](#21-quick-overview)
2. [Components ke 2 parts](#22-components-ke-2-parts)
3. [Logical Entities](#23-logical-entities)
4. [Tangible Entities (Technologies)](#24-tangible-entities-technologies)
5. [System ka superficial overview](#25-system-ka-superficial-overview)
6. [Building analogy](#26-building-analogy)
7. [Key Takeaways](#video-2-key-takeaways-quick-revision)
8. [Self-Test Questions](#video-2-self-test-questions)

## 2.1 Quick Overview

**Video ka goal:** System ke basic building blocks (**components**) samjhana. Components ko do hisson mein baanta gaya hai: **logical entities** aur **tangible entities**. End mein sab ko jodke ek superficial system diagram dikhaya gaya hai.

## 2.2 Components ke 2 parts

| Type | Matlab | Examples |
|---|---|---|
| **Logical entities** | System ke "concepts / layers", ye kya kaam karte hain | Database, Application, Communication protocols, Presentation, Infrastructure |
| **Tangible entities** | Wo real technologies jinse ye logical cheezein banti hain | MySQL, MongoDB, React, APIs, AWS, etc. |

## 2.3 Logical Entities

### 1) Database

- Saare systems **data** par bane hote hain, data system ka crux hai.
- Database ek technology hai jo data **store** karti hai, taaki baad mein users ko available ho sake.
- Users database se **read, write, fetch, store** karte hain.

### 2) Application (Application layer)

- Users seedha database se baat nahi karte, beech mein **application / service** hoti hai.
- Ye aapko mobile apps, desktop apps, websites ke form mein dikhti hai.
- Application = ek machine par chal raha code. Database = dusri machine par chal raha code.

### 3) Communication Protocols

Do machines ko aapas mein baat karni hai, iske liye protocols chahiye.

| Level | Kaise communicate hota hai |
|---|---|
| Network level (machine to machine) | HTTP, TCP, etc. |
| Software level (service to service) | Requests in the form of **APIs, RPCs** (aage detail mein aayega) |

### 4) Presentation

- Wo layer jisse **user system se interact** karta hai: mobile app, desktop app, web app.
- Har system mein presentation layer **ho bhi sakti hai, nahi bhi**.
- Example jahan nahi hoti: ek **logging system** jo sirf application ke logs collect karta hai.

### 5) Infrastructure

- Upar ke saare components kisi **computers / instances** par chalte hain.
- Ye instances cloud providers dete hain: **AWS, Google Cloud Platform (GCP), Azure**.
- Ye sab milke system ki **infrastructure requirements** banate hain.

> `⚠️ Correction` Video mein instances ko "physical computers / hardware instances" bola gaya. Cloud mein instances zyadatar **virtual machines (VMs)** hote hain jo provider ke physical servers par chalte hain (aur aajkal containers bhi common hain). Physical machine (bare metal) bhi milti hai, lekin default "instance" = VM.

> `⚠️ Correction` (imprecise) "Har system ka core database hota hai" thoda zyada general hai. Zyadatar systems ko data store karna padta hai, lekin kuch systems (jaise pure stateless compute service ya proxy) mein khud ka database nahi hota. Rule of thumb: jahan data persist karna ho wahan database aata hai.

## 2.4 Tangible Entities (Technologies)

| Logical component | Technologies / options |
|---|---|
| Database | MongoDB, MySQL, Cassandra, Redis, etc. |
| Application / Services + communication | APIs, RPCs, etc. |
| Presentation | Front-end frameworks (React, Angular, Vue, Ember, etc.); Android aur iOS ke liye apna native code |
| Security | Security mechanisms aur protocols (data secure rakhne aur attacks se bachne ke liye) |
| Infrastructure | Cloud providers ke instances (AWS, GCP, Azure) |

> `Extra` **Database types (taaki naam yaad rahe):**
>
> | Database | Type | Ek line |
> |---|---|---|
> | MySQL | Relational (SQL) | Tables, rows, fixed schema |
> | MongoDB | Document (NoSQL) | JSON jaise documents |
> | Cassandra | Wide-column (NoSQL) | Bahut zyada writes aur scale ke liye |
> | Redis | Key-value, in-memory | Bahut fast, caching mein common |
>
> Inka detail aage ke videos mein aayega.

> `Extra` **API ek interface hai, technology style alag hoti hai:** API ko implement karne ke popular styles REST, gRPC (ek modern RPC framework) aur GraphQL hain. Video mein sirf "APIs, RPCs" bola gaya hai.

> `🔄 Update` **Frontend:** Ember ab kaafi kam use hota hai. Aajkal common: **React, Angular, Vue, Svelte**, aur unke upar meta-frameworks jaise **Next.js**. **Mobile:** native (Kotlin for Android, Swift for iOS) ke saath **cross-platform** options jaise **Flutter** aur **React Native** bhi bahut common hain.

> `🔄 Update` **Protocols:** HTTP/1.1 aur HTTP/2 TCP par chalte hain, lekin **HTTP/3** (RFC 9114) **QUIC** par chalta hai jo **UDP** ke upar bana hai. To "HTTP = TCP" ab hamesha sach nahi.

> `🔄 Update` **Security:** Data in transit encrypt karne ke liye ab **TLS** use hota hai (latest widely used version **TLS 1.3**). Purana **SSL** deprecated hai.

## 2.5 System ka superficial overview

```
 [ Presentation: Desktop app / Website / Mobile app ]
                     |
                     |  network (HTTP, TCP) -- blue lines
                     v
 [ Application / Services  (machine A) ] <--- APIs / messages ---> [ other services ]
                     |
                     |  read / write
                     v
 [ Database  (machine B) ]

 ===== ye sab Infrastructure (AWS / GCP / Azure) ke instances par deployed hai =====
```

- User presentation layer se interact karta hai, wo backend ki applications se baat karti hai.
- Applications database se data exchange karti hain.
- Machines network par aapas mein connected hain, services APIs / messages se baat karti hain.
- Ye sab cloud provider (infrastructure) ke andar hai.
- Ye sirf **bahut superficial** picture hai, course aage badhega to ye detail mein bharta jayega.

## 2.6 Building analogy

| Building | Software system |
|---|---|
| Walls, floors, terrace | Applications, databases |
| Fire escape / exit strategy | Failure handling, security |
| Electrical supply | Infrastructure |
| (dusre parts) | **Caches, load balancers, client interfaces, network requests, security layer** |

Aage ke videos mein har component ko **alag karke detail mein** samjhenge, aur end mein sab ko jodke bada system banayenge.

> `Extra` Video ke end mein **cache** aur **load balancer** ka naam aaya hai, lekin logical entities ki list mein nahi tha. Inke saath **CDN** aur **message queue** bhi aise common components hain jo bade systems mein aate hain.

## Video 2: Key Takeaways (Quick Revision)

1. Components do type ke hote hain: **logical entities** aur **tangible entities (technologies)**.
2. Logical entities: **Database, Application, Communication protocols, Presentation, Infrastructure**.
3. Database data store karta hai, application database aur user ke beech ka layer hai.
4. Machines **network protocols (HTTP, TCP)** se, services **APIs / RPCs** se baat karti hain.
5. **Presentation layer optional** hai (e.g. logging system mein zaroori nahi).
6. Infrastructure cloud providers (**AWS, GCP, Azure**) se aata hai.
7. Technologies: DB (MongoDB, MySQL, Cassandra, Redis), frontend (React, etc.), native Android/iOS, security protocols.
8. Cloud "instances" zyadatar **VMs** hote hain, physical machines nahi.
9. HTTP/3 UDP-based QUIC par chalta hai, aur encryption ke liye TLS (SSL nahi).
10. Superficial system: Presentation -> Application -> Database, sab Infrastructure par.

## Video 2: Self-Test Questions

1. Components ke do parts kaun se hain? Har ek ka ek line mein matlab batao.
2. 5 logical entities ke naam batao.
3. Application layer ki zaroorat kyun padti hai? User seedha database se kyun nahi baat karta?
4. Network level aur software level communication mein kya fark hai? Har ek ka example do.
5. Presentation layer har system mein kyun zaroori nahi? Ek example do.
6. Infrastructure kya hai aur kaun se providers use hote hain?
7. Cloud "instance" physical hardware hota hai ya VM? (`⚠️ Correction`)
8. MySQL, MongoDB, Cassandra, Redis ke type batao. (`Extra`)
9. HTTP/3 kis transport protocol par chalta hai? (`🔄 Update`)
10. Superficial system diagram ko apne words mein draw karke explain karo.

---
---

# Video 3: Client-Server Architecture (Pseudocode)

## Table of Contents

1. [Quick Overview](#31-quick-overview)
2. [Client aur Server, basic idea](#32-client-aur-server-basic-idea)
3. [Thick Client vs Thin Client](#33-thick-client-vs-thin-client)
4. [Tiers: 2-tier, 3-tier, N-tier](#34-tiers-2-tier-3-tier-n-tier)
5. [Kaise decide karein?](#35-kaise-decide-karein)
6. [Key Takeaways](#video-3-key-takeaways-quick-revision)
7. [Self-Test Questions](#video-3-self-test-questions)

## 3.1 Quick Overview

**Video ka goal:** Client-server architecture samjhana: client kya hai, server kya hai, **thick vs thin client** mein kya fark hai, aur **2-tier, 3-tier, N-tier** architectures kya hote hain aur kab kaunsa choose karein.

## 3.2 Client aur Server, basic idea

**Basic flow:** Client server se koi data **request** karta hai (image, text file, etc.), server wo data **respond** karta hai.

```
 Client  ---- request ---->  Server
 Client  <--- response ----  Server
```

**Analogy (broker):** Main broker se poochta hoon "is property ka price kya hai?", broker bata deta hai. Yahan sirf data aaya-gaya.

### Kabhi kabhi logic bhi lagta hai

| Scenario | Kya hota hai | Broker analogy |
|---|---|---|
| Sirf data serve karna | Server data return karta hai | "Is property ka price kya hai?" |
| **Logical manipulation** | Server data par calculation / filtering karke result deta hai | "Mera ye budget hai, kaunse houses afford kar sakta hoon?" -> broker filtered list deta hai |

Example: Website jahan **yearly income** daalte ho aur server calculation karke **tax kitna banega** bata deta hai.

Video ke hisaab se is basic setup mein **logic aur data dono server par** baithte hain, ise video ne **two-tier** bola hai.

> `⚠️ Correction` (imprecise) Video "client + server (jisme logic aur data dono hain)" ko two-tier bolta hai. Standard definition mein **tier** ka matlab hai physical / deployment level par alag machines ka layer. Classic **2-tier** = **Client (presentation + aksar logic) <-> Database server**. Yahan "application server" naam ka alag beech ka tier nahi hota. Video ka simple model samajhne ke liye theek hai, lekin interview mein classic definition use karna.

## 3.3 Thick Client vs Thin Client

Teen cheezein hoti hain: **Presentation, Logic, Data**. Logic kahan baithta hai, us par fark padta hai.

| | **Thick Client** | **Thin Client** |
|---|---|---|
| Logic / processing kahan? | **Client side** par | **Server side** par |
| Client ki responsibility | Zyada | Kam (isi liye "thin") |
| Examples | Microsoft Outlook, video editing software, desktop video games | Netflix, Hotstar (presentation hai, lekin zyadatar processing backend par) |

```
 THICK CLIENT                          THIN CLIENT
 +-----------------------+            +-----------------------+
 | Presentation + LOGIC  |            | Presentation          |
 +-----------------------+            +-----------------------+
            |                                    |
            v                                    v
 +-----------------------+            +-----------------------+
 | Server (data)         |            | Server (LOGIC + data) |
 +-----------------------+            +-----------------------+
```

> `Extra` **Layer vs Tier:** **Layer** = code ka logical separation (presentation, logic, data). **Tier** = un layers ko **alag machines / servers** par deploy karna. Ek app 3 layers ki ho sakti hai lekin ek hi machine par (1 tier) chal sakti hai.

> `🔄 Update` Aajkal thick/thin ka fark dhundhla ho gaya hai. Modern web apps (SPA jaise React apps) aur mobile apps browser/phone par kaafi logic chalate hain (thick jaisa), phir bhi backend se APIs ke through data lete hain. Isliye ise strict black and white ke bajaye **spectrum** ki tarah samjho.

## 3.4 Tiers: 2-tier, 3-tier, N-tier

### Two-tier

```
 [ Client ]  <---->  [ Server: logic + data ]
```

Ya (thick client case) logic client par, data server par.

### Three-tier

Jab **processing bahut zyada** ho ya **data bahut heavy** ho, to server wale layer ko do hisson mein todte hain:

```
 [ Client / Presentation ]  <---->  [ Application / Logic ]  <---->  [ Database / Data ]
        Tier 1                            Tier 2                          Tier 3
```

Ab teen alag machines / layers hain: presentation, logic (application), data (database).

### N-tier

Jab application **bahut bada aur complex** ho aur 3 layers kaafi nahi hote, to beech mein aur layers aati hain:

```
 [ Client ] -> [ Load Balancer / Proxy ] -> [ Application ] -> [ Cache ] -> [ Database ]
```

- Logic aur data ke beech: **caching layer**
- Client aur logic ke beech: **load balancers, proxies**

Inhe alag videos mein detail mein padhenge.

> `Extra` **Real examples:**
> - **2-tier:** purani desktop app jo seedha database se connect hoti hai
> - **3-tier:** zyadatar web apps (e.g. React frontend + Node.js / Django backend + PostgreSQL database)
> - **N-tier:** bade systems (load balancer, API gateway, cache, message queue, multiple services, database)

## 3.5 Kaise decide karein?

| Situation | Choice |
|---|---|
| Sirf images / text files serve karni hain, kam logic | **Basic client-server (2-tier)**, server data store karke serve karta hai |
| Rich GUI + zyada processing **user ke end par** (desktop video games, etc.) | **Thick client** |
| Rich GUI chahiye lekin processing **server par** | **Thin client** |
| Bahut processing + bahut data | **3-tier**: presentation, logic, data alag alag |
| Bahut bada user base, 3 layers kaafi nahi | **N-tier**: load balancer, caching, etc. |

> `⚠️ Correction` Video mein "rich GUI lekin processing server par" wale case ke liye **"thick client"** bola gaya (transcript mein "thick lines" likha aaya hai, ye garbled hai), jo ghalat hai. Sahi term **thin client** hai, kyunki processing server par ho rahi hai. Transcript mein "quick client" = **thick client** samajhna.

> `Extra` **Desktop vs online games:** Video ne bola "online nahi, desktop video games" thick client ke liye. Online multiplayer games **hybrid** hote hain: rendering client par, game state aur rules server par.

## Video 3: Key Takeaways (Quick Revision)

1. **Client request karta hai, server respond karta hai**, ye client-server ka basic idea hai.
2. Server sirf data de sakta hai, ya **logic / calculation** karke result bhi de sakta hai.
3. **Thick client:** logic client par (Outlook, video editors, desktop games).
4. **Thin client:** logic server par (Netflix, Hotstar).
5. Teen cheezein: **presentation, logic, data**, inka placement architecture decide karta hai.
6. **2-tier:** client aur server (classic: client <-> database).
7. **3-tier:** presentation / application (logic) / database alag alag.
8. **N-tier:** beech mein cache, load balancer, proxy jaise extra layers.
9. Rich GUI + server-side processing = **thin client** (video ke "thick" slip ko theek karo).
10. Layer = logical separation, tier = physical separation.

## Video 3: Self-Test Questions

1. Client-server architecture ka basic flow apne words mein samjhao.
2. Broker analogy se "sirf data" aur "logic wala" case alag alag samjhao.
3. Thick client aur thin client mein kya fark hai? Har ek ke 2 examples do.
4. Netflix thin client kyun maana jata hai?
5. 2-tier aur 3-tier architecture mein kya difference hai? Diagram draw karo.
6. Kab 2-tier se 3-tier mein jaana padta hai?
7. N-tier mein kaun se extra layers aate hain? (Kam se kam 3 naam batao.)
8. Rich GUI + server-side processing ke liye kaunsa client choose karoge? (`⚠️ Correction`)
9. Layer aur tier mein kya fark hai? (`Extra`)
10. Aajkal thick/thin ka fark dhundhla kyun ho gaya hai? (`🔄 Update`)

---
---

# Video 4: Forward and Reverse Proxies (Pseudocode)

## Table of Contents

1. [Quick Overview](#41-quick-overview)
2. [Proxy kya hota hai?](#42-proxy-kya-hota-hai)
3. [Forward Proxy](#43-forward-proxy)
4. [Reverse Proxy](#44-reverse-proxy)
5. [Forward vs Reverse, comparison](#45-forward-vs-reverse-comparison)
6. [Caveats (Cons)](#46-caveats-cons)
7. [Key Takeaways](#video-4-key-takeaways-quick-revision)
8. [Self-Test Questions](#video-4-self-test-questions)

## 4.1 Quick Overview

**Video ka goal:** Proxy kya hai, **forward proxy**, **reverse proxy**, dono mein difference, unke pros/cons aur use cases samjhana.

## 4.2 Proxy kya hota hai?

> **Proxy = "on behalf of".** Jab bhi proxy suno, "kisi ki taraf se" socho.

| Analogy | Proxy kaun? |
|---|---|
| Class attend nahi kar sakte, dost aapki jagah **attendance** deta hai | Dost |
| Broker se privacy ke reason se seedha baat nahi karni, apne **assistant** se apartments search karwate ho | Assistant |

Client-server architecture mein 2 type ke proxies hote hain: **forward proxy** aur **reverse proxy**.

## 4.3 Forward Proxy

**Kya hai:** Ek machine jo **client aur server ke beech, client ki taraf** baithti hai aur **client ki taraf se server se baat karti hai**.

```
 Client(s) ---> [ FORWARD PROXY ] ---> Internet / Server
 Client(s) <--- [ FORWARD PROXY ] <--- Internet / Server
 
 (Server ko sirf proxy ka IP dikhta hai, client ka nahi)
```

- Client **kabhi server se seedha baat nahi karta**.
- Client -> proxy ko request, proxy -> server ko request, proxy response collect karke client ko deta hai.

### Use cases

| Use case | Kaise kaam karta hai |
|---|---|
| **Anonymity** | Server ko client ka IP nahi pata, sirf proxy ka IP pata hai |
| **Traffic control / monitoring** | Institutions mein bahut saare clients ka traffic ek proxy se control aur monitor hota hai |
| **Site blocking** | Certain sites ka access block karna |
| **Caching** | Responses forward proxy par cache hote hain |

> `Extra` **Forward proxy ke types (anonymity level ke hisaab se):**
> - **Transparent proxy:** client ko / server ko pata chal sakta hai, original IP header mein pass ho sakta hai
> - **Anonymous proxy:** client ka IP chhupata hai, lekin proxy hone ka pata chal sakta hai
> - **Elite (high-anonymity) proxy:** na client ka IP, na proxy hone ka pata chalta hai
>
> **Tools:** Squid is a popular forward proxy.

> `⚠️ Correction` (imprecise) "Forward proxy se anonymity milti hai" sab proxies ke liye sach nahi. Kayi proxies `X-Forwarded-For` jaise headers se **original client IP aage pass kar dete hain**. Anonymity proxy ke type par depend karti hai.

> `Extra` **Proxy vs VPN:** Proxy aam taur par ek app / browser level par traffic route karta hai, aur zaroori nahi ki encrypt kare. **VPN** poore device ka traffic encrypted tunnel se bhejta hai.

## 4.4 Reverse Proxy

**Kya hai:** Wahi proxy server jab **server side** par baithta hai aur saare servers ke liye **middleman** ban jata hai.

```
 Client ---> [ REVERSE PROXY ] ---> Server 1
                    |-----------> Server 2
                    |-----------> Server 3
 Client <--- [ REVERSE PROXY ] <--- (response)

 (Client ko sirf proxy ka address pata hai, servers ke IPs nahi)
```

- Yahan **servers ki anonymity** hoti hai.
- Client ko kisi bhi server ka IP nahi pata, sirf proxy pata hai.

### Use cases

| Use case | Kaise kaam karta hai |
|---|---|
| **Traffic control** | Incoming traffic ko manage karna |
| **Load balancing** | Requests ko multiple servers mein baantna (aage detail mein) |
| **Caching** | Servers ke responses cache karna |
| **DDoS mitigation** | Servers outside world ko exposed nahi, sirf proxy exposed hai |
| **SSL encryption** | Encryption proxy par handle hoti hai |

> `🔄 Update` Video "SSL encryption" bolta hai. Aajkal **SSL deprecated** hai aur **TLS** use hota hai. Reverse proxy par isko **TLS termination** kehte hain: proxy encryption handle karta hai, backend servers ko decrypted traffic milta hai.

> `Extra` **Reverse proxy tools aur examples:** **Nginx, HAProxy, Envoy**; CDNs (jaise Cloudflare) bhi ek tarah se globally distributed reverse proxies hain. Kubernetes mein **Ingress controller** aur microservices mein **API gateway** bhi reverse proxy ka hi roop hain.

> `Extra` **Load balancer = specialised reverse proxy** jo main kaam requests ko servers mein distribute karna karta hai.

> `⚠️ Correction` (imprecise) "Reverse proxy se DDoS mitigate hota hai kyunki sirf proxy exposed hai" adhoora hai. Isse **origin servers hide** hote hain, lekin proxy khud target ban sakta hai, aur origin IP kisi aur raste se leak ho jaye to protection bekar ho jati hai. Practical DDoS protection ke liye **rate limiting, filtering aur scalable / managed DDoS protection** bhi chahiye.

## 4.5 Forward vs Reverse, comparison

| Point | Forward Proxy | Reverse Proxy |
|---|---|---|
| Kahan baithta hai | **Client side** | **Server side** |
| Kiski taraf se baat karta hai | **Client ki** taraf se | **Server(s) ki** taraf se |
| Kisko hide karta hai | **Client** (IP) | **Servers** (IPs) |
| Kaun jaanta hai ki proxy hai | Client ko pata hota hai | Client ko aam taur par pata nahi |
| Use cases | Anonymity, monitoring, blocking, caching | Load balancing, caching, DDoS protection, SSL / TLS |

**Yaad rakhne ka trick:**
- **Forward** = client ki taraf se -> **client ko** hide karta hai.
- **Reverse** = server ki taraf se -> **servers ko** hide karta hai.

## 4.6 Caveats (Cons)

| Caveat | Detail |
|---|---|
| **Blocked sites bypass** | Country / organization / workplace ke blocked sites proxy se access ho sakte hain. Ye useful bhi hai, lekin organization ke rules bypass hote hain, isliye har jagah sahi nahi. |
| **Reverse proxy = Single Point of Failure (SPOF)** | Agar reverse proxy fail ho gaya to saare servers unreachable ho jaate hain, ye **bottleneck** bhi ban sakta hai. |

> `Extra` **SPOF kaise kam karein:** **multiple reverse proxies** chalao (redundancy) aur unke aage **failover** (e.g. DNS ya virtual IP) rakho, taaki ek fail ho to dusra traffic sambhal le.

> `Extra` Bypass karna kuch jagah **policy ya law ke khilaf** bhi ho sakta hai, to use karne se pehle rules check karo.

**Conclusion (video ke hisaab se):** Proxies **security, privacy aur traffic handling** ke liye important elements hain.

## Video 4: Key Takeaways (Quick Revision)

1. **Proxy = "on behalf of"** (kisi ki taraf se kaam karne wala).
2. **Forward proxy:** client ki taraf baithta hai, client ki jagah server se baat karta hai.
3. Forward proxy mein server ko **client ka IP nahi** dikhta, sirf proxy ka.
4. Forward proxy use cases: **anonymity, monitoring, blocking, caching**.
5. **Reverse proxy:** server side par baithta hai, saare servers ka middleman.
6. Reverse proxy mein client ko **servers ke IPs nahi** pata hote.
7. Reverse proxy use cases: **load balancing, caching, DDoS mitigation, SSL / TLS**.
8. Forward proxy **client** ko hide karta hai, reverse proxy **servers** ko hide karta hai.
9. Reverse proxy ek **single point of failure** ban sakta hai, isliye redundancy rakho.
10. Proxy se blocked sites bypass ho sakti hain, lekin ye organization ke rules ke khilaf ho sakta hai.

## Video 4: Self-Test Questions

1. Proxy ka matlab "on behalf of" kaise hai? Ek real-life example do.
2. Forward proxy ka flow diagram draw karke samjhao.
3. Forward proxy ke 4 use cases batao.
4. Reverse proxy ka flow diagram draw karo aur batao ki kaun hide hota hai.
5. Forward aur reverse proxy mein 3 differences batao.
6. Reverse proxy DDoS mitigation mein kaise madad karta hai? Iski limits kya hain? (`⚠️ Correction`)
7. Reverse proxy ke SPOF problem ko kaise solve karoge? (`Extra`)
8. Load balancer aur reverse proxy ka kya relation hai? (`Extra`)
9. SSL aur TLS mein se aaj kaunsa use hota hai, aur "TLS termination" kya hai? (`🔄 Update`)
10. Proxy aur VPN mein kya fark hai? (`Extra`)