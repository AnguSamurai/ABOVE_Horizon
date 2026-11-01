---
layout: default
title: "Horizon Summary: 2026-11-01 (EN)"
date: 2026-11-01
lang: en
---

> From 192 items, 15 important content pieces were selected

---

**Technology News**
1. [Jepsen Finds Severe Transactional Flaws in ParticleDB 1.1.4](#item-tech-news-1) ⭐️ 8.0/10
2. [Linux TCP Use-After-Free CVE-2026-98432 Rated CVSS 9.8](#item-tech-news-2) ⭐️ 8.0/10
3. [Researchers Detail ChatGPT Account Takeover Chain, $5,000 Bounty](#item-tech-news-3) ⭐️ 8.0/10

**Financial News**
1. [伊朗称四艘油轮在霍尔木兹海峡爆炸起火](#item-finance-news-1) ⭐️ 8.0/10
2. [Musk Spends $445.77m on US Midterms, Report Says](#item-finance-news-2) ⭐️ 8.0/10
3. [美国批准向乌克兰出售500枚“爱国者”导弹，盟友承担21亿美元费用](#item-finance-news-3) ⭐️ 7.0/10
4. [Binance Faces Reported $6.3 Billion Crypto Heist](#item-finance-news-4) ⭐️ 7.0/10
5. [China&\#x27;s Economic Activity Slowed Sharply in October, WSJ Reports](#item-finance-news-5) ⭐️ 7.0/10
6. [Fitch Lowers France&\#x27;s Credit Outlook to Negative](#item-finance-news-6) ⭐️ 7.0/10
7. [Investors Shift from Growth Stocks to Bonds on AI Reliance Worries](#item-finance-news-7) ⭐️ 7.0/10
8. [Iran&\#x27;s Supreme Leader Warns of Unrestricted Retaliation if Attacked](#item-finance-news-8) ⭐️ 7.0/10
9. [Tusk Vows to Continue Poland Judiciary Overhaul](#item-finance-news-9) ⭐️ 7.0/10
10. [Report: Trump support reached 90 of 184 US coal plants](#item-finance-news-10) ⭐️ 7.0/10

**Technology Blog**
1. [How GCC Lowers Switch Statements](#item-tech-blog-1) ⭐️ 7.0/10

**AI Creator Radar**
1. [DeepSeek Harness 发布 Super-agent 架构探索：Router 与 Worker 双层协作](#item-ai-creator-1) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Jepsen Finds Severe Transactional Flaws in ParticleDB 1.1.4](https://jepsen.io/analyses/particledb-1.1.4) ⭐️ 8.0/10

Jepsen&\#x27;s analysis of ParticleDB 1.1.4 reports frequent, profound transactional anomalies, including loss of committed writes, internal consistency violations, and G1a \(Aborted Read\), G1b \(Intermediate Read\), and P4 \(Lost Update\) anomalies. In the append workload, successfully appended values routinely disappeared from later reads of a given key. The report catalogs 96 issues, from crashes, deadlocks, and data loss to partially invisible rows, WHERE 4 = 5 evaluating incorrectly, dropped tables re-emerging in distorted forms, confused columns, and strings turning into integers. Jepsen recommends users halt further deployment of ParticleDB and migrate to other databases as soon as possible, and consider rebuilding database state from more reliable sources.

hackernews · Hacker News · Oct 31, 13:39 · [Discussion](https://news.ycombinator.com/item?id=50316100)

**「Background」** Jepsen analyses test whether a database delivers the isolation and consistency guarantees it advertises, typically by running concurrent workloads and checking the observed histories against formal anomaly definitions. ParticleDB 1.1.4 claimed Postgres compatibility and offered Snapshot Isolation via its occ-v3 and zero-copy-occ transaction modes, Serializability via serializable-ssi, and Strong Serializability via table-2pl, according to the analysis. The audit&\#x27;s findings are therefore measured against those advertised modes rather than a generic baseline.

**「Impact」** Operators running ParticleDB 1.1.4 should treat stored data as potentially unreliable: Jepsen advises halting deployment, migrating to another database, and checking or rebuilding state from more reliable sources where available. The report also notes that ParticleDB&\#x27;s home page advertised a TLA+ formal proof, but no TLA+ specification was available during the collaboration, so it is unclear what properties were proven or whether they described ParticleDB as built.

**「Community Discussion」** Commenters reacted to the severity of the findings, with one summarizing the report&\#x27;s language as describing &quot;a library of confusion&quot; and another attributing the outcome to &quot;vibecoding a database.&quot; One commenter drew a broader distinction between software that is correct by construction, where failures are generally local bugs, and software that is incorrect by construction and works only through luck and workarounds in most code paths.

<details><summary>References</summary>
<ul>
<li><a href="https://jepsen.io/analyses/particledb-1.1.4">Jepsen: ParticleDB 1.1.4</a></li>

</ul>
</details>

**Tags**: `#databases`, `#distributed-systems`, `#transactional-consistency`, `#jepsen`, `#testing`

---

<a id="item-tech-news-2"></a>
### [Linux TCP Use-After-Free CVE-2026-98432 Rated CVSS 9.8](https://atlasum.net/blog/cve-2026-98432-linux-ipv4-tcp-uaf) ⭐️ 8.0/10

A critical Linux IPv4 TCP use-after-free vulnerability, tracked as CVE-2026-98432, carries a CVSS score of 9.8. Community notes say MPTCP is not required for the flaw, that internet exploitability is unlikely because most ISP routers drop packets carrying IP options, and that a successful exploit requires multiple CPU cores processing packets, so single-core systems or those pinning packet processing to one core are not affected. Commenters report that Ubuntu and Red Hat had not yet published patches, citing the vendors&\#x27; CVE pages. The source item provides no primary advisory text, so the technical details here rest on the linked blog and community discussion.

hackernews · Hacker News · Oct 31, 19:16 · [Discussion](https://news.ycombinator.com/item?id=50319143)

**「Background」** The flaw sits in the Linux kernel&\#x27;s IPv4 TCP handshake path, specifically during SYNACK processing, and affects kernel versions 4.4 and later, according to AWS&\#x27;s security bulletin. Red Hat&\#x27;s advisory describes it as a use-after-free in the IPv4 networking subsystem that a remote, unauthenticated attacker could trigger via a race condition during TCP connection request processing to achieve remote code execution.

**「Impact」** Administrators of multi-core Linux servers should treat this as unpatched until distro updates appear, since commenters report no Ubuntu or RHEL fix at the time of discussion. Dropping packets with IP options is described as a partial mitigation at best, per Red Hat, and not a full fix.

**「Community Discussion」** Commenters debated the title edit that dropped &quot;Linux,&quot; noting the flaw affects Linux only and not BSD, macOS, or Windows. Others questioned why Ubuntu and RHEL, both marketed for servers, lacked patches, and one reader asked for CVE RSS feeds after this entry failed to appear in their monitoring list.

<details><summary>References</summary>
<ul>
<li><a href="https://aws.amazon.com/security/security-bulletins/2026-160-aws/">CVE-2026-98432 - Linux kernel IPv4 TCP use-after-free Issue</a></li>
<li><a href="https://access.redhat.com/security/vulnerabilities/RHSB-2026-016">RHSB-2026-016 Use-after-free - kernel IPv4 (CVE-2026-98432 ...</a></li>
<li><a href="https://www.sentinelone.com/vulnerability-database/cve-2026-98432/">CVE-2026-98432: Linux Kernel Use-After-Free Vulnerability</a></li>

</ul>
</details>

**Tags**: `#linux`, `#security`, `#vulnerability`, `#tcp`, `#cve`

---

<a id="item-tech-news-3"></a>
### [Researchers Detail ChatGPT Account Takeover Chain, $5,000 Bounty](https://www.parameter.ai/labs/we-found-a-gap-at-openai) ⭐️ 8.0/10

Researchers at Parameter.ai published a write-up describing how they chained frontend weaknesses to take over ChatGPT accounts. According to the account quoted in the discussion, OpenAI confirmed both frontends rejected the reported messages, resolved the issue, and paid a total bounty of $5,000. The attack required the user to click a link, a condition that limits its practical reach. The source item itself contains no technical detail, so the specific vulnerability chain cannot be independently described here.

hackernews · Hacker News · Oct 31, 10:30 · [Discussion](https://news.ycombinator.com/item?id=50314699)

**「Background」** The write-up describes a chain that bypassed ChatGPT&\#x27;s sandbox and Content Security Policy so that a crafted share link could run code in a victim&\#x27;s chatgpt.com session. According to coverage of the report, OpenAI fixed the issue on October 26, 2026, across two frontend versions, with CSP changes on October 23 blocking part of the chain during rollout, and rated the report P1 with a $5,000 bounty.

**「Impact」** The reported chain required the victim to click a link, so the practical exposure depends on user interaction rather than silent compromise. Commenters also flagged a separate concern about remote file-system access in the ChatGPT desktop app for users who have started a &quot;Work&quot; chat, though that claim comes from a linked discussion rather than the researchers&\#x27; write-up. The $5,000 total bounty is the main point of contention: one commenter argues small payouts may discourage future reports.

**「Community Discussion」** Commenters disputed the size of the $5,000 payout, with yellow\_lead and Kuyawa arguing it is too low and may discourage future reports. lxgr linked the finding to a separate report of remote file-system access in the ChatGPT desktop app after a &quot;Work&quot; chat has been started. zahlman said the write-up&\#x27;s explanation is hard to follow, particularly the JSONP section, which reads as a description of the protection rather than the bypass.

<details><summary>References</summary>
<ul>
<li><a href="https://www.parameter.ai/labs/we-found-a-gap-at-openai">Do the Math: How We Took Over ChatGPT Accounts - parameter.ai</a></li>
<li><a href="https://explainx.ai/blog/chatgpt-share-link-account-takeover-mathlive-postmessage-csp-youtube-jsonp-fixed-oct-26-2026">ChatGPT Account Takeover via Share Link: P1 Bug, $5,000 ...</a></li>
<li><a href="http://ai-tldr.dev/releases/parameter-chatgpt-share-xss-account-takeover/">ChatGPT Shared-Link Flaw — one click ran… | AI/TLDR</a></li>

</ul>
</details>

**Tags**: `#security`, `#vulnerability-research`, `#ChatGPT`, `#web-security`, `#bug-bounty`

---

## Financial News

<a id="item-finance-news-1"></a>
### [伊朗称四艘油轮在霍尔木兹海峡爆炸起火](https://www.chinanews.com.cn/gj/2026/10-31/10723785.shtml) ⭐️ 8.0/10

据伊朗媒体报道，伊朗伊斯兰革命卫队表示，10月30日有四艘“违规”油轮在霍尔木兹海峡爆炸起火。报道未说明涉事船只身份、伤亡情况、起火原因，也未说明是否影响航运或石油供应。

rss · 中新网-要闻 · Oct 31, 01:40

**「Background」** The Strait of Hormuz is a narrow waterway through which a large share of the world&\#x27;s seaborne oil passes. The report follows earlier accounts of tankers being stopped and set on fire there after taking an unauthorized route, amid a war between Iran and the United States and ongoing mediation talks.

**「Impact」** The Strait of Hormuz is a key passage for global oil trade, and shipping through it has been largely blocked by Iran since late February 2026, when the US and Israel launched an air war against Iran \(tool-2-1\). Oil prices have stayed elevated on expectations the conflict will escalate, according to Saul Kavonic of MST Marquee, cited by Reuters \(tool-2-2\). Even so, tankers were still moving substantial volumes of crude through the strait before this incident, unlike March, when exports collapsed \(tool-2-3\).

<details><summary>References</summary>
<ul>
<li><a href="https://www.euronews.com/2026/10/30/irans-revolutionary-guard-reports-two-tankers-on-fire-in-strait-of-hormuz-as-talks-continu">Iran’s Revolutionary Guard reports three tankers on fire in Strait of ...</a></li>
<li><a href="https://www.presstv.co.uk/Detail/2026/10/30/779541/irgc-supertanker-catches-fire-after-taking-unauthorized-hormuz-route">Three offending tankers catch fire in Strait of Hormuz after defying...</a></li>
<li><a href="https://www.aljazeera.com/news/liveblog/2026/10/31/iran-war-live-oil-tankers-hit-in-hormuz-trump-says-conflict-will-end-soon">Iran war live: Oil tankers hit in Hormuz ; Trump says... | Al Jazeera</a></li>
<li><a href="https://en.wikipedia.org/wiki/2026_Strait_of_Hormuz_crisis">2026 Strait of Hormuz crisis - Wikipedia</a></li>
<li><a href="https://nypost.com/2026/10/30/world-news/three-oil-tankers-explode-in-strait-of-hormuz-iran/">Ships carrying 2M barrels of oil hit mines, explode in Strait of ...</a></li>
<li><a href="https://www.cnbc.com/2026/10/30/tanker-attack-strait-hormuz-iran-war-oil.html">Tankers defy Iran attacks to keep crude oil flowing through Hormuz</a></li>

</ul>
</details>

**Tags**: `#oil`, `#shipping`, `#Iran`, `#Strait of Hormuz`, `#energy supply`

---

<a id="item-finance-news-2"></a>
### [Musk Spends $445.77m on US Midterms, Report Says](https://www.theguardian.com/us-news/ng-interactive/2026/oct/31/elon-musk-midterms-spending-visualized) ⭐️ 8.0/10

Elon Musk has given at least $445.77m to Republican-aligned political action committees and groups in the current US midterm election cycle, according to Federal Election Commission data as of 29 October cited by a Guardian analysis. The report says this makes him the largest single-cycle political donor in modern US history.

rss · The Guardian · Oct 31, 10:00

**「Background」** Political action committees, or PACs, are organizations that pool donations to spend on elections, and US campaigns must disclose their donors and spending to the Federal Election Commission. The Guardian&\#x27;s figure covers donations since last year and is based on filings available as of 29 October, so later contributions would not be included.

**「Impact」** The scale of the donations makes Musk the Republicans&\#x27; most prominent financial backer this cycle, giving him unusual potential influence over the party&\#x27;s campaigns and, if its candidates win, over policy debates that affect his companies.

**Tags**: `#political spending`, `#campaign finance`, `#Elon Musk`, `#US midterms`, `#FEC data`

---

<a id="item-finance-news-3"></a>
### [美国批准向乌克兰出售500枚“爱国者”导弹，盟友承担21亿美元费用](https://www.chinanews.com.cn/gj/2026/10-31/10723789.shtml) ⭐️ 7.0/10

美国国务院于2026年10月30日宣布，批准向乌克兰出售500枚“爱国者”导弹及相关设备，总价值21亿美元，费用“完全由合作伙伴和盟友承担”。

rss · 中新网-要闻 · Oct 31, 01:51

**「Background」** The State Department&\#x27;s approval covers 500 Patriot Advanced Capability-3 \(PAC-3\) Missile Segment Enhancement missiles, which Ukraine requested, with the $2.1 billion estimated cost funded entirely by partners and allies, according to the State Department notice.

**「Impact」** The allies and partners footing the $2.1 billion bill will bear the budget cost, while the order adds to demand for Patriot PAC-3 MSE interceptors and related support work. Ukraine has separately asked for 500 interceptors from existing stockpiles during the 2026–2027 winter, with allied inventories replenished later through new production, according to The Defense News.

<details><summary>References</summary>
<ul>
<li><a href="https://www.state.gov/releases/bureau-of-political-military-affairs/2026/10/ukraine-patriot-advanced-capability-3-pac-3-missiles/">Ukraine – PATRIOT Advanced Capability-3 (PAC-3) Missiles</a></li>
<li><a href="https://www.reuters.com/business/aerospace-defense/us-approves-21-billion-patriot-missile-sale-ukraine-2026-10-30/">US approves $2.1 billion Patriot missile sale to Ukraine ...</a></li>
<li><a href="https://www.state.gov/releases/bureau-of-political-military-affairs/2026/10/ukraine-patriot-advanced-capability-3-pac-3-missiles/">Ukraine – PATRIOT Advanced Capability-3 (PAC-3) Missiles</a></li>
<li><a href="https://www.thedefensenews.com/US-Approves-21-Billion-Patriot-Missile-Sale-to-Ukraine-Funded-by-Allied-Nations/">US Approves $2.1 Billion Patriot Missile Sale to Ukraine ...</a></li>

</ul>
</details>

**Tags**: `#defense procurement`, `#Ukraine`, `#US foreign policy`, `#arms sales`, `#geopolitics`

---

<a id="item-finance-news-4"></a>
### [Binance Faces Reported $6.3 Billion Crypto Heist](https://www.nytimes.com/2026/10/31/technology/binance-hack-crypto-north-korea.html) ⭐️ 7.0/10

The New York Times reports that Binance, the world&\#x27;s largest crypto exchange, dealt with what it describes as the largest crypto heist in history, reportedly $6.3 billion, during a frantic 24-hour response. The FBI says North Korea was responsible for the hack.

rss · NYT · Oct 31, 22:19

**「Background」** The FBI says North Korea was responsible for the theft, which reportedly occurred on 29 October 2026 and is described as the largest crypto heist ever, surpassing the $1.5 billion Bybit hack in 2025. Binance held about $163 billion in assets as of 2025, according to Wikipedia.

**「Who is affected」** Binance says about $3 billion of the $6.3 billion in affected assets has been frozen and that losses will be covered, so the direct exposure for exchange users depends on how much is recovered. Crypto prices fell after the breach, affecting holders across the market.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/2026_Binance_hack">2026 Binance hack - Wikipedia</a></li>
<li><a href="https://www.fbi.gov/investigate/cyber/alerts/2026/north-korea-responsible-for-6-billion-binance-attack">North Korea Responsible for $6 Billion+ Binance Attack — FBI</a></li>
<li><a href="https://www.cnbc.com/2026/10/29/circle-tether-freeze-funds-impacted-by-potential-binance-security-issue.html">Binance hack : $ 6 . 3 billion impacted in record crypto theft</a></li>
<li><a href="https://cointelegraph.com/news/live-updates-binance-63b-hack-linked-to-north-koreas-tradertraitor">Binance ’s Record $ 6 . 3 B Crypto Hack as It Happened</a></li>
<li><a href="https://finance.yahoo.com/markets/article/bitcoin-drops-to-76000-as-binance-hack-spooks-investors-tether-circle-freeze-assets-083406383.html">Binance hacked for record $ 6 . 3 billion , withdrawals suspended after...</a></li>

</ul>
</details>

**Tags**: `#crypto`, `#cybersecurity`, `#Binance`, `#financial crime`, `#markets`

---

<a id="item-finance-news-5"></a>
### [China&\#x27;s Economic Activity Slowed Sharply in October, WSJ Reports](https://www.wsj.com/world/asia/china-economic-activity-loses-steam-sharply-in-october-5990ffe0?mod=rss_worldnews) ⭐️ 7.0/10

The Wall Street Journal reported that China&\#x27;s economic activity slowed sharply in October, a significant signal for the world&\#x27;s second-largest economy. The supplied text contains only the headline, with no figures, baselines, or sector detail.

rss · WSJ · Oct 31, 01:50

**「Background」** The Wall Street Journal report gives no figures, so the size of the October slowdown cannot be verified from the supplied text. Earlier October data cited by ING showed retail sales growth easing to 2.9% year on year, a 0.1 percentage point decline from September, while industrial production also slowed.

<details><summary>References</summary>
<ul>
<li><a href="https://think.ing.com/articles/china-october-data-shows-fading-momentum/">Chinese data shows momentum fading into the final... | ING THINK</a></li>

</ul>
</details>

**Tags**: `#China economy`, `#macroeconomic data`, `#economic slowdown`, `#global markets`

---

<a id="item-finance-news-6"></a>
### [Fitch Lowers France&\#x27;s Credit Outlook to Negative](https://www.wsj.com/world/europe/fitch-lowers-frances-outlook-to-negative-from-stable-27de23a3?mod=rss_worldnews) ⭐️ 7.0/10

Fitch cut France&\#x27;s credit outlook to negative from stable, saying conditions have deteriorated since its August review due to weaker growth, higher borrowing costs and a wider deficit. The agency did not provide figures or baselines in the cited account.

rss · WSJ · Oct 31, 00:27

**「Background」** Fitch affirmed France&\#x27;s long-term credit rating at A+ while changing the outlook from stable to negative, meaning the rating could be downgraded if conditions worsen. The agency said the deterioration since its August 2026 review — weaker growth, higher borrowing costs and a wider deficit — worsens debt dynamics from an already weak starting point.

**「What it means」** A negative outlook signals Fitch sees a rising chance of a downgrade, which could push up the interest rate France pays on new debt and add to its borrowing costs; French 10-year bond yields had already climbed above 4.9% and the debt-to-GDP ratio stood at 119%, according to the FT.

<details><summary>References</summary>
<ul>
<li><a href="https://www.fitchratings.com/research/sovereigns/fitch-revises-france-outlook-to-negative-affirms-at-a-30-10-2026">Fitch Revises France&#x27;s Outlook to Negative; Affirms at &#x27;A+&#x27;</a></li>
<li><a href="https://en.fnnews.com/news/202610311004450686">Fitch Cuts France’s Credit Rating Outlook to ‘Negative ...</a></li>
<li><a href="https://www.zerohedge.com/economics/frances-debt-alarm-gets-louder-fitch-cuts-outlook-negative-surprise-warning">France &#x27;s Debt Alarm Gets Louder: Fitch Cuts Outlook To... | ZeroHedge</a></li>
<li><a href="https://www.ft.com/content/e7c1da68-aed3-471d-911f-0b6086a327ec?syn-25a6b1a6=1">France meets fiscal reality with a crunch</a></li>

</ul>
</details>

**Tags**: `#sovereign credit rating`, `#France`, `#fiscal deficit`, `#Fitch`, `#eurozone`

---

<a id="item-finance-news-7"></a>
### [Investors Shift from Growth Stocks to Bonds on AI Reliance Worries](https://www.ft.com/content/56b0d5fa-829c-47b1-b07b-b4be18f60151?syn-25a6b1a6=1) ⭐️ 7.0/10

Investors are reportedly moving money out of growth bets and back into bonds, according to the Financial Times, as concern grows that the US economy leans too heavily on AI and tech spending. The report gives no figures on the size of the shift.

rss · Financial Times · Oct 31, 14:00

**「Background」** The move marks a return to bonds after a long sell-off, as investors grow concerned that the US economy leans too heavily on technology and AI spending. Sector rotation—shifting money between industry groups as conditions change—has been complicated in the 2024–2026 cycle by rate cuts coinciding with an AI capital-spending boom, per Brimind Invest.

**「Who is affected」** Investors shifting from growth assets into bonds are also buying into a credit market increasingly shaped by AI-related debt, as large tech companies fund infrastructure spending with borrowing, which raises concentration risk for passive investors, according to J.P. Morgan Asset Management.

<details><summary>References</summary>
<ul>
<li><a href="https://brimindinvest.com/blog/sp500-sector-rotation-guide-2026">S&amp;P 500 Sector Rotation 2026: Fed Rate Cut Playbook</a></li>
<li><a href="https://am.jpmorgan.com/wr/en/asset-management/institutional/insights/market-insights/market-updates/on-the-minds-of-investors/ai-the-new-bond-giant/">AI: The new bond giant | J.P. Morgan Asset Management</a></li>

</ul>
</details>

**Tags**: `#AI investment`, `#market rotation`, `#US economy`, `#bonds`, `#tech sector`

---

<a id="item-finance-news-8"></a>
### [Iran&\#x27;s Supreme Leader Warns of Unrestricted Retaliation if Attacked](https://www.ft.com/content/77370477-62df-4499-9ab6-4063d3e361bd?syn-25a6b1a6=1) ⭐️ 7.0/10

Iran&\#x27;s supreme leader, Ayatollah Khamenei, told military commanders that any attack on Iran would draw an &quot;immediate&quot; response with no &quot;geographical limitations,&quot; according to the Financial Times. The warning comes as Qatari mediators work to prevent a feared US-Israeli bombing campaign.

rss · Financial Times · Oct 31, 13:38

**「Background」** The warning comes eight months after a joint US-Israeli bombing campaign triggered full-scale hostilities, and follows a February campaign that killed Khamenei&\#x27;s father and several senior Iranian officials, according to reports.

**「Who is affected」** A wider conflict could disrupt energy trade through the Strait of Hormuz, a key shipping route for oil and gas, affecting global fuel prices and households and businesses that depend on them.

<details><summary>References</summary>
<ul>
<li><a href="https://www.yahoo.com/news/world/articles/khamenei-orders-iran-military-response-162154037.html?fr=sycsrp_catchall">Khamenei orders Iran military response &quot;without geographical ...</a></li>
<li><a href="https://indianexpress.com/article/world/iran-mojtaba-khamenei-military-response-geographic-limits-us-israel-10945119/">Iran’s Mojtaba Khamenei warns US, Israel of response without ...</a></li>
<li><a href="https://en.wikipedia.org/wiki/2026_Strait_of_Hormuz_crisis">2026 Strait of Hormuz crisis - Wikipedia</a></li>
<li><a href="https://www.bbc.com/news/topics/cx2jyv8j8gwt">US - Israel war with Iran | Latest News and Updates | BBC News</a></li>
<li><a href="https://www.congress.gov/crs_external_products/R/PDF/R45281/R45281.6.pdf">Iran Conflict and the Strait of Hormuz : Impacts on Oil , Gas, and...</a></li>

</ul>
</details>

**Tags**: `#geopolitics`, `#Iran`, `#Middle East conflict`, `#energy markets`, `#diplomacy`

---

<a id="item-finance-news-9"></a>
### [Tusk Vows to Continue Poland Judiciary Overhaul](https://www.ft.com/content/d49a7943-fc11-45cb-bcf2-f5876c3c381d?syn-25a6b1a6=1) ⭐️ 7.0/10

Poland&\#x27;s prime minister, Donald Tusk, said in a televised address on Saturday that he will press ahead with a contested overhaul of the constitutional court, saying &quot;in certain matters, there can be no compromise.&quot; The move follows the suspension of the court&\#x27;s president, Bogdan Święczkowski, and his deputy by a group of government-appointed judges, which the opposition calls an institutional coup.

rss · Financial Times · Oct 31, 22:51

**「Background」** The standoff is the latest escalation in a dispute over the Constitutional Tribunal&\#x27;s legitimacy dating back to a 2015 court crisis, and it follows the October 30 suspension of tribunal president Bogdan Święczkowski and his deputy by government-appointed judges. President Karol Nawrocki has refused to swear in five of the eight judges elected this year by the prime minister&\#x27;s parliamentary majority, leaving the court&\#x27;s membership contested.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Suspension_of_Bogdan_%C5%9Awi%C4%99czkowski">Suspension of Bogdan Święczkowski - Wikipedia</a></li>
<li><a href="https://www.theguardian.com/world/2026/oct/31/riot-police-deployed-to-polands-constitutional-court-after-judge-suspended">Riot police deployed to Poland ’s constitutional court ... | The Guardian</a></li>
<li><a href="https://brusselssignal.eu/2026/10/tusk-moves-to-take-over-constitutional-court-by-force/">Tusk moves to take over constitutional court by force - Brussels Signal</a></li>

</ul>
</details>

**Tags**: `#Poland`, `#judiciary`, `#rule of law`, `#politics`, `#institutional risk`

---

<a id="item-finance-news-10"></a>
### [Report: Trump support reached 90 of 184 US coal plants](https://www.theguardian.com/us-news/2026/oct/31/trump-coal-plants-taxpayer-dollars) ⭐️ 7.0/10

An Environmental Defense Fund analysis found that the Trump administration supported 90 of the 184 grid-connected US coal plants through $950 million in funding and Clean Air Act exemptions, according to The Guardian. The analysis says the support included requirements that some plants stay online past their retirement dates.

rss · The Guardian · Oct 31, 13:00

**「Background」** The Environmental Defense Fund, an advocacy group, says the administration issued Clean Air Act exemptions in 2025 to 154 units at 70 coal plants, waiving the 2024 Mercury and Air Toxics Standards that tightened limits on hazardous air pollutants. The administration has also moved to keep coal plants running past planned retirement dates, reversing a decline it had targeted.

**「Impact」** The report links taxpayer money and looser pollution rules to keeping nearly half of the country&\#x27;s grid-connected coal plants running, which affects the plants&\#x27; operators and nearby communities exposed to their emissions.

<details><summary>References</summary>
<ul>
<li><a href="https://coalcosts.edf.org/">Coal Costs Americans — Tracking Expensive Giveaways to Coal ...</a></li>
<li><a href="https://www.edf.org/media/trump-administration-has-handed-giveaways-nearly-half-us-coal-plants">Trump administration has handed giveaways to nearly half of U ...</a></li>
<li><a href="https://www.theguardian.com/us-news/2026/feb/27/trump-coal-plant-air-pollution-rules">Most US coal plants could meet air pollution rules. Trump weakened...</a></li>

</ul>
</details>

**Tags**: `#energy policy`, `#coal industry`, `#environmental regulation`, `#government subsidies`, `#US politics`

---

## Technology Blog

<a id="item-tech-blog-1"></a>
### [How GCC Lowers Switch Statements](https://xoranth.net/gcc-switch/) ⭐️ 7.0/10

hackernews · Hacker News · Oct 31, 08:02 · [Discussion](https://news.ycombinator.com/item?id=50314085)

**「Background」** Switch statements can be compiled into jump tables or decision trees, and the choice has real consequences for speed and compile time. The article examines how GCC makes that choice, while commenters add practical experience with the tradeoffs.

**「Solution」** The explainer walks through GCC&\#x27;s switch lowering, where the compiler may emit a jump table or a decision tree, even when a tree may not be the better choice. Commenters supply concrete counterexamples to any simple preference for jump tables. One reports that replacing a switch in .NET&\#x27;s System.HashCode with a decision tree was significantly faster, though the details are no longer at hand. Another notes that a very large switch over MAC-address manufacturers compiled fine in LLVM without optimizations but took roughly half an hour with them enabled, while GCC was faster; the commenter ultimately used perfect hashing, which compiled much faster. A third argues that GCC and Clang still lack perfect hashing for large sparse switches, saying a recent implementation in their own C compiler took a single day and is especially useful for Unicode work, and that an LLVM patch was rejected a decade ago while GCC Unicode patches sit in branches. A further comment questions why a jump table would indirect through another jump rather than reference the case targets directly, and another observes that GCC misses a simplification in a sparse switch that divides the input by eight before jumping, because that would route seven values per case to function calls instead of the default case.

**「Takeaway」** The discussion suggests that switch lowering is a genuine engineering tradeoff rather than a solved problem: decision trees can beat jump tables in practice, and large sparse switches expose compile-time and code-generation limits that perfect hashing might address.

**Tags**: `#compilers`, `#gcc`, `#code-generation`, `#optimization`, `#switch-statements`

---

## AI Creator Radar

<a id="item-ai-creator-1"></a>
### [DeepSeek Harness 发布 Super-agent 架构探索：Router 与 Worker 双层协作](https://www.ifanr.com/1687026?utm_source=rss&amp;utm_medium=rss&amp;utm_campaign=) ⭐️ 7.0/10

DeepSeek Harness 团队发表技术文章《Super-agent 设计探索：迈向更自主的 Agent 系统》，提出由 Router 和 Worker 组成的双层架构，目标是让 Agent 持续在线、并行处理多任务并主动响应群聊、GitHub、邮件等事件。团队称已在内部研发协作中试用，例如在群聊中无人 @ 时识别缺陷、后台复现并提交 Pull Request。文章强调这仍是工程实践中的架构探索，部分设计以 dsh-superagent-prototype 原型插件实现，并非正式独立产品。初步实验使用约 300 条合成消息、其中约 20 条为真实工作请求，Super-agent 任务完成时间 p50 为 12.4 分钟、p95 为 15.7 分钟，传统单 Session 方案 p95 为 29.5 分钟；但缓存读取 Token 增加约 37%，且实验未直接评估真实编码质量。

rss · 爱范儿 · Oct 31, 13:59

**「为何值得关注」** 文章把 Agent 的瓶颈从单任务能力转向人类同时管理多个会话的注意力上限，并给出可验证的调度实验数据。需要区分的是：内部试用和原型插件已经发生，而大规模应用、长期记忆与安全隐私等问题仍被团队列为待解挑战。

**「内容角度」** 可做角度：从“人类只能同时跟进 3 到 5 个活跃 Session”这一观察出发，拆解 Router/Worker 双层架构如何把会话管理变成系统内部细节，并对照实验中 p95 从 29.5 分钟降至 15.7 分钟与 Token 成本增加 37% 的取舍。

**Tags**: `#DeepSeek`, `#AI Agent`, `#Agent 架构`, `#开发者工具`, `#技术探索`

---