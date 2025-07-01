---
title: Small Bug - Big Impact
marp: true
paginate: true
center: false
_class: lead
---
<style type="text/css">
   html, body {
    background-color: #0f172a;
  }
  section {  
    background-color: #0f172a; 
    color: #f8fafc;  
    font-family: 'JetBrains Mono', monospace;  
  }  
  h1, h2, h3 {  
    color: #38bdf8;  
  }  
  img {  
    border-radius: 12px;  
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);  
  }  
</style>



# ❓ Code Quiz: Small Bug – Big Impact
## BTPEX SRM Developer Forum

----

> “All bugs in this presentation are based on actual events.” 🐞🎬

----

You litteraly could say: 

> “The following code has actually taken down rockets, banks, and billions.” 💥

---

# 💻 Quiz
```c
if ((err = SSLVerify(...)) != 0)
    goto fail;
    goto fail;
```
> ❓ What’s the issue on this c Code?

----

### ✅ Fix
```c
if ((err = SSLVerify(...)) != 0)
    goto fail;
```
> delete second ```goto```

----

# 💻 Quiz: Apple "goto fail" (2014)

### ⚠️ Impact
- SSL certificate verification skipped
- Affected iOS and macOS
- Allowed MitM attacks over HTTPS
- Shook public trust in Apple security

---

# ☁️ Quiz
```bash
ecs-cli down --cluster "s3-*"
```
> ❓ What went wrong with bash command?

----
### ✅ Fix

```bash
# Intended:
ecs-cli down --cluster "s3-a"
# Actual:
ecs-cli down --cluster "s3-*"
```

> eliminate wildcard on input agrument

### ✅ additional fix

```bash
read -p "Confirm cluster: $CLUSTER_NAME? (yes/no): " ans
[[ "$ans" != "yes" ]] && exit 1
```

----
# ☁️ Quiz: AWS S3 Outage (2017)

### ⚠️ Impact
- Disabled entire region’s S3 infrastructure
- Took down major platforms: GitHub, Slack, Trello
- Estimated economic loss in the hundreds of millions

---

# 💥 Quiz
```c
double time = t * 0.1;  // using fixed-point approximation
```
> ❓ Why is this dangerous in long-running systems?

----

### ✅ Fix
```c
uint64_t ticks = t;
double time = ticks * 0.1;  // use precise conversion
```

----
# 💥 Quiz: Patriot Missile Drift (1991)

### ⚠️ Impact
- System time drifted ~0.34s after 100h
- Caused missile defense failure
- 28 soldiers killed in attack

---

# 💼 Quiz
```java
balance = Math.round(balance * 100) / 100.0;
```
> ❓ What’s the risk with this rounding logic?

----

### ✅ Fix
```java
int balanceCents = depositCents - withdrawalCents;
```

----
# 💼 Quiz: Horizon Accounting Scandal

### ⚠️ Impact
- 700+ postmasters falsely accused and convicted
- Based on flawed accounting system
- Legal battle, reputational damage, ruined lives

---

# ☁️ Quiz
```yaml
database_url: ""
```
> ❓ Why did this config cause massive failure?

----

### ✅ Fix
```python
if not config.database_url:
    raise ConfigError("Missing database URL")
```

----
# ☁️ Quiz: Google Cloud Config Outage (2025)

### ⚠️ Impact
- Global services went offline
- Due to unvalidated critical config fields (null / empty check)
- Highlighted fragility of cloud infrastructure

---

# ✈️ Quiz
```text
CATIA V4 (german team)
CATIA V5 (french team)
```

> ❓ What’s the risk of using different CAD tools?

----
### ⚠️ Problem
```text
CATIA V4: cable = 1000 mm
CATIA V5: required = 1001 mm
```

----
### ✅ Fix
- Standardize to CATIA V5
- Validate full digital mockups (DMU)
- Sync ECAD-MCAD data across teams

----
# ✈️ Quiz: Airbus A380 – CAD Version Mismatch

### ⚠️ Impact
- 530 km of cabling incorrect
- Massive rework, 2-year delay
- Billions of euros in cost

---

<!-- SAP HANA Java Leak -->

# ☕️ Quiz
```java
try {
    Connection conn = dataSource.getConnection();
    // processing code that throws an exception...
    conn.close();
} catch (Exception e) {
    logger.error("Failure", e);
}
```
> ❓ What’s the critical mistake in this try block?

----

### ✅ Fix
```java
Connection conn = null;
try {
    conn = dataSource.getConnection();
    // work with conn
} catch (Exception e) {
    logger.error("Failure", e);
} finally {
    if (conn != null) {
      try { 
        conn.close(); 
      } catch (SQLException ignore) {
        // handle / log closing-issue
      }
    }
}
```

----
### ✅ even better Fix

```java
try (Connection conn = dataSource.getConnection()) {
    // safe processing
} catch (Exception e) {
    logger.error("Failure", e);
}
```

----
# ☕️ Quiz: SAP HANA Java Connection Leak (~2017)

### ⚠️ Impact
- Happened in **SAP IoT context** under load
- Unclosed HANA connections accumulated silently
- After ~500 connections → **DB crashed**
- Crash occurred after ~15 min of runtime
- Required debug analysis across services and logs
- several ours of service outage for customers

---

# 🧠 Key Takeaways

✅ Automated testing catches edge cases early  
✅ Four-eyes principle for pull requests prevents human oversight  
✅ Consistent tooling & formats reduce integration errors  
✅ Config validation is as critical as code  
✅ Legacy code reuse must be validated in new contexts  
✅ Edge-case awareness (overflows, precision, units) is vital  
✅ Communication across teams and systems prevents disasters  
✅ Float ≠ money or time — use precise datatypes

----

# 🙌 Thanks for Playing!
### BTPEX SRM Developer Forum

🎯 Which failure surprised you the most?
What could you bring into your daily development practice?

---
