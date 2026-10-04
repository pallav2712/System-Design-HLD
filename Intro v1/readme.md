# Video 1: Course Overview & Intro to System Design (Pseudocode)

> Playlist: System Design Primer Course
> Notes ki language: Hinglish (Roman script)
> Tag guide: `Extra` = jo video mein nahi tha, revision ke liye add kiya hai
> `⚠️ Correction` = video mein jo galat ya imprecise bola gaya, uska sahi version
> `🔄 Update` = video purana hai, ab jo latest hai wo yahan likha hai

## Table of Contents

1. [Quick Overview](#1-quick-overview)
2. [Course Overview (Kiske liye, kya milega)](#2-course-overview-kiske-liye-kya-milega)
3. [System kya hota hai?](#3-system-kya-hota-hai)
4. [Design kya hota hai?](#4-design-kya-hota-hai)
5. [System Design ki zaroorat kyun?](#5-system-design-ki-zaroorat-kyun)
6. [Course ka approach](#6-course-ka-approach)
7. [Key Takeaways (Quick Revision)](#key-takeaways-quick-revision)
8. [Self-Test Questions](#self-test-questions)

---

## 1. Quick Overview

**Video ka goal:** System Design Primer course ka intro dena, aur teen basic sawalon ka jawab dena: **System kya hai? Design kya hai? System design ki zaroorat kyun hai?**

**Kya cover hua:**

| Topic | Ek line mein |
|---|---|
| Course overview | Beginners ke liye fundamentals, real-life examples + quizzes + exercises |
| System | Components ka collection jo users ki requirements serve karta hai |
| Design | Requirements samajhna + components choose karna + unka interaction decide karna |
| Why system design | Large scale systems complex hote hain, trade-offs aur failures samajhne padte hain |
| Course approach | Components ko alag alag todo, pros/cons samjho, phir jodke large system banao |

---

## 2. Course Overview (Kiske liye, kya milega)

### Ye course kiske liye hai?

- Computer science students
- Job change karne wale engineers
- Industry mein already kaam karne wale log
- Basically koi bhi jo **system design ke fundamentals / basic building blocks** seekhna chahta hai

### Course ka format

```
Video (concepts + real-life examples)
        |
        v
Quiz + Exercises (har video ke end mein)
        |
        v
Discussion (Slack / comments)
```

### Course ke end mein kya aana chahiye?

- System design ka **process** better samajh aaye
- **Fundamental concepts** clear hon
- Aage jaake **large scale systems** build karna seekh sako

> `Extra` **Prerequisites:** Speaker ne agenda mein bola "what do you need to know in advance" lekin video mein actually bataya nahi. Generally ye cheezein aani chahiye:
> - Basic programming (koi bhi ek language)
> - Basic networking (client-server, HTTP, IP/DNS ka idea)
> - Database ka basic idea (SQL tables, queries)
> - Thoda OS/web basics (process, thread, request-response)
>
> Inme se kuch nahi aata to bhi chalega, course fundamentals se start hota hai, bas inka rough idea ho to speed badhegi.

> `🔄 Update` Video mein discussion ke liye **Slack** mention hua hai. Ye ek purana mention hai, aaj wo community active hai ya nahi, ye notes ke liye zaroori nahi. Doubt ho to playlist ke comments ya GitHub discussions use karo.

---

## 3. System kya hota hai?

**Definition:** System ek loosely used term hai. Matlab: software ya technology ka ek **architecture / collection** jo aapas mein **interact** karta hai, taaki ek certain set of **users** ko unki certain **requirements** ke saath serve kar sake.

### Examples

| Type | Examples |
|---|---|
| Software systems | Instagram (image sharing), WhatsApp (texting), Netflix / Hotstar (streaming) |
| Real-world systems | Buildings, hotels, hospitals, theaters |

### Sab systems mein kya common hai?

Sab systems **components / modules** se bane hote hain jo mil-jul ke kaam karte hain.

**Analogy (building vs software):**

| | Building | Software system |
|---|---|---|
| Basic components | Walls, floors, ceilings, electrical supply, water supply | Servers, databases, networks, application code |
| Components same? | Haan, har building mein lagbhag same | Haan, building blocks same hote hain |
| Fark kahan? | Users aur unki requirements alag (hospital vs hotel) | Users aur requirements alag (Netflix vs WhatsApp) |

### System ko define karne wale 3 factors

```
        +-------------------+
        |  1. Users         |  (kaun use karega?)
        +-------------------+
                 |
        +-------------------+
        |  2. Requirements  |  (unhe kya chahiye?)
        +-------------------+
                 |
        +-------------------+
        |  3. Components    |  (kya use karke banaye?)
        +-------------------+
                 |
                 v
              SYSTEM
```

> `Extra` **Requirements ke 2 type:**
> - **Functional requirements:** system *kya* karega (e.g. photo upload, message send, video play)
> - **Non-functional requirements:** system *kaisa* perform karega (e.g. speed/latency, availability, scalability, reliability, security)
>
> System design mein dono ka dhyan rakhna padta hai, aur aksar non-functional requirements hi design decide karte hain.

> `Extra` **Common software building blocks** (aage ke videos mein aayenge): client, server, database, cache, load balancer, CDN, message queue, API gateway, etc.

---

## 4. Design kya hota hai?

**Definition (video ke hisaab se):** Design ek **process** hai jisme:

1. User requirements samajhte hain
2. Components, modules aur software technologies **select** karte hain
3. Ye decide karte hain ki wo kaise **intertwined** honge aur ek dusre se kaise **communicate** karenge
4. Different **constraints aur concerns** ko factor mein lete hain

Ye poora process hi **design** kehlata hai.

### Same components, alag design

Basic building blocks same ho sakte hain, lekin do alag systems ka design bahut alag dikhta hai.

| Real-world analogy | Software analogy |
|---|---|
| Duplex ka design vs Skyscraper ka design | Static website (1-2 videos serve karne wali) vs Netflix jaisa streaming platform |

> `Extra` **Design ke 2 levels** (interviews mein bahut poochha jata hai):
> - **HLD (High Level Design):** big picture, major components aur unka interaction (e.g. client, load balancer, servers, DB, cache)
> - **LLD (Low Level Design):** andar ki detail, classes, schema, APIs, code-level structure
>
> Ye course mostly **HLD** side par focus karta hai.

> `⚠️ Correction` (imprecise) Video ka definition "design = components select karna" thoda simplified hai. Design mein ye bhi shamil hota hai: **data model**, **APIs / interfaces**, **data flow**, aur sabse important **trade-offs** (e.g. consistency vs availability, cost vs performance). Sirf components choose karna design ka ek hissa hai, poora design nahi.

---

## 5. System Design ki zaroorat kyun?

**Kyun popular topic hai?** Kyunki large scale systems build karna **bahut complicated** hota hai. Isme chahiye:

- Experience
- Expertise
- Software technologies ki knowledge

### Real world mein kaise hota hai?

Real world mein ye kaam **ek insaan nahi karta**, team karti hai. Lekin ek engineer ko ye pata hona chahiye:

| Engineer ko kya pata hona chahiye |
|---|
| Components kya hain |
| **Trade-offs** kya hain |
| Kaun si **problems solve** karni hain |
| Systems **kahan fail** ho sakte hain |
| Un failures ko **kaise handle** karein |
| Kaun se **concerns aur constraints** address karne hain |

> `⚠️ Correction` (imprecise) Video mein lagta hai ki system design sirf "larger scale aur larger users" ke liye hai. Sach ye hai ki system design **har scale par** hota hai, chhote app ke liye bhi. Bas scale badhne par design ke decisions zyada critical aur complex ho jate hain.

> `Extra` **Mantra:** System design mein koi "perfect" answer nahi hota, sirf **trade-offs** hote hain. Har choice ka ek faida aur ek nuksaan hota hai, aur requirements ke hisaab se best choice badalti hai.

> `🔄 Update` Aaj ke systems mein **cloud-managed services** (managed databases, queues, serverless, etc.) aur AI/LLM based components bhi common building blocks ban gaye hain. Fundamentals (trade-offs, scalability, failure handling) wahi rehte hain, bas available building blocks badh gaye hain.

---

## 6. Course ka approach

```
Step 1: System ke components ko ALAG alag todo
            |
            v
Step 2: Har component ko akele samjho
        (kyun use hota hai, kahan use hota hai,
         pros aur cons kya hain)
            |
            v
Step 3: Sabko JODKE ek large scale system banao
```

Ye "pull apart, understand, combine" approach hai.

---

## Key Takeaways (Quick Revision)

1. **System** = software/technology ka collection jo interact karke certain users ko certain requirements ke saath serve karta hai.
2. Real-world systems (building, hospital) aur software systems (Netflix, WhatsApp) dono components se bante hain.
3. System teen cheezon se define hota hai: **Users, Requirements, Components**.
4. Basic components same hote hain, lekin users aur requirements alag to system alag.
5. **Design** = requirements samajhna + components choose karna + unka interaction decide karna + constraints dekhna.
6. Same building blocks se bhi design alag banta hai (duplex vs skyscraper, static site vs Netflix).
7. System design **complex** skill hai kyunki large systems mein trade-offs aur failures handle karne padte hain.
8. Engineer ko **components, trade-offs, failure points aur constraints** ka knowledge hona chahiye.
9. Course ka approach: components alag alag samjho (pros/cons ke saath), phir combine karke large system banao.
10. Har video ke baad **quiz + exercises**, aur discussion Slack/comments par.

---

## Self-Test Questions

1. System ki definition apne words mein batao. Ek software aur ek real-world example do.
2. Kisi bhi system ko define karne wale 3 factors kaun se hain?
3. Building ke components aur software system ke components ka analogy samjhao.
4. Design kya hota hai? Video ke hisaab se iske kaun se steps hain?
5. Duplex aur skyscraper ke design ka example kis concept ko explain karta hai? Iska software equivalent kya hai?
6. System design ek popular aur zaroori skill kyun hai?
7. Ek engineer ko system design karte waqt kaun si 5 cheezein pata honi chahiye?
8. Functional aur non-functional requirements mein kya fark hai? Har ek ka ek example do. (`Extra`)
9. HLD aur LLD mein kya difference hai? (`Extra`)
10. Is course ka approach (pull apart, understand, combine) 3 steps mein explain karo.