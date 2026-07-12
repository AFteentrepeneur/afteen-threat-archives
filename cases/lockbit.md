# The Rise and Fall (and Return) of LockBit

**Video:** TBD
**Status:** In Research
**Last updated:** July 12, 2026

## Summary

LockBit emerged in September 2019, initially calling itself "ABCD" ransomware, and grew into the most prolific ransomware-as-a-service (RaaS) operation in the world — extorting an estimated $500 million from more than 2,500 victims globally before international law enforcement seized its infrastructure in February 2024 under **Operation Cronos**. The takedown was historic in scale, but LockBit's near-immediate partial resurgence made it just as important a lesson in ransomware resilience as it was a law enforcement win.

## Timeline

| Date | Event | Source |
|---|---|---|
| Sept 2019 | LockBit emerges as "ABCD" ransomware, encrypting files with the .abcd extension | Hivepro |
| Jan 2020 | LockBit begins operating as an affiliate-based RaaS variant | CISA |
| June 2021 | LockBit 2.0 ("Red") introduces a dedicated data-exfiltration module | Hivepro |
| Oct 2021 | A Linux/VMware ESXi variant expands LockBit's reach beyond Windows | Hivepro |
| March 2022 | LockBit 3.0 ("Black") launches with compile-time customization options | Hivepro |
| Jan 2023 | "LockBit Green," built on leaked Conti encryptor code, targets cloud services | Akamai |
| 2022–2023 | LockBit becomes the most active ransomware group by victim count on its leak site for two consecutive years, with victims including Boeing, the UK Ministry of Defence, and TSMC | Searchlight Cyber |
| Aug 2023 | LockBit 3.0 affiliates begin exploiting the Citrix Bleed vulnerability (CVE-2023-4966) for initial access | CISA |
| Feb 19–20, 2024 | Operation Cronos, a 10-country law enforcement task force led by the UK NCA and FBI, seizes LockBit's dark web infrastructure; 34 servers, 14,000 rogue accounts, and 200 cryptocurrency accounts are seized or frozen, alongside two arrests and five indictments | Akamai, Arctic Wolf |
| Feb 24, 2024 | LockBit's leak site returns online after roughly four days, restored from backup servers that weren't running the vulnerable PHP version exploited by law enforcement | Picus Security |
| May 7, 2024 | The US, UK, and Australia jointly identify and sanction Dmitry Yuryevich Khoroshev, a Russian national, as LockBit's key administrator and developer | Improved-Move |

## Techniques Used

- **Initial access:** Affiliates most commonly exploited known, unpatched vulnerabilities in public-facing systems — most notably CVE-2023-4966 ("Citrix Bleed") in NetScaler ADC and Gateway appliances. Law enforcement itself is believed to have used a known, six-month-old PHP remote-code-execution vulnerability (CVE-2023-3824) to gain access to LockBit's own servers — a detail that underlines how consistently unpatched software was the common thread on both sides of this story.
- **Execution & evasion:** LockBit 3.0 required a password argument to decrypt and run its own executable, meaning affiliates without the correct password couldn't execute it — a technique that also hindered signature-based malware detection since the encrypted binary varied by key. It could also force a reboot into Safe Mode to bypass endpoint antivirus and disable Windows Defender via Group Policy XML files.
- **Living-off-the-land & tooling:** Affiliates repurposed legitimate freeware and open-source tools for credential dumping, network scanning, and remote access, alongside professional penetration-testing tools like Metasploit and Cobalt Strike.
- **Data exfiltration:** Affiliates commonly used anonymous file-sharing services to move stolen data out before encryption began, supporting LockBit's double-extortion model.
- **Double and secondary extortion:** Beyond the initial victim, affiliates sometimes extorted that victim's own customers with secondary ransomware or threats to leak the customer's data — extending the blast radius of a single breach through the supply chain.
- **Affiliate recruitment:** As a RaaS operation, LockBit's core team didn't run attacks directly — it sold access to its ransomware and infrastructure to independent affiliates in exchange for a cut of ransom profits, which is part of why the group proved so hard to fully dismantle: taking down infrastructure doesn't remove the affiliates who know how to rebuild around it.

## Patterns Identified

1. **Unpatched, known vulnerabilities remain the dominant entry point.** Citrix Bleed had been public for months before LockBit affiliates weaponized it at scale — this is a recurring theme across ransomware groups, not unique to LockBit.
2. **RaaS structures are resilient by design.** Because LockBit's affiliates operated independently using shared tooling, seizing the core infrastructure didn't eliminate the people capable of causing harm — it just temporarily removed their platform.
3. **Infrastructure takedowns and attribution take different timelines.** The technical seizure happened in February 2024; the named-individual sanctioning of Khoroshev didn't land until May 2024 — a reminder that "the group was taken down" and "the person responsible was identified" are two separate milestones, often reported as one.
4. **Law enforcement is increasingly using the same tradecraft as attackers.** Operation Cronos succeeded in part by exploiting an unpatched vulnerability in LockBit's own infrastructure — turning the group's tactics back on itself.

## Defensive Lessons

- **Patch public-facing infrastructure promptly**, especially VPN gateways, remote access appliances, and anything internet-facing — Citrix Bleed was known and patchable for months before exploitation at scale.
- **Segment backups and keep them offline or immutable.** LockBit's affiliates actively targeted Volume Shadow Copies and backup infrastructure to prevent recovery without payment.
- **Monitor for living-off-the-land tooling**, not just known malware signatures — legitimate admin and pentesting tools were core to LockBit affiliate operations precisely because they blend into normal activity.
- **Plan for the supply-chain extension of an attack**, not just the initial victim — LockBit affiliates were documented extorting a target's customers, not just the target itself.
- **Report incidents even after paying (or not paying).** Law enforcement's ability to build cases like Operation Cronos depends heavily on victim reporting and shared indicators, not just proactive detection.

## Sources

1. [Learning from the LockBit Takedown](https://www.akamai.com/blog/security/learning-from-the-lockbit-takedown) — Akamai
2. [A Timeline of Events: Operation Cronos and LockBit](https://slcyber.io/blog/a-timeline-of-events-operation-cronos-and-lockbit/) — Searchlight Cyber
3. [LockBit Takedown & Operation Cronos: A Long-Awaited PsyOps Against Ransomware](https://analyst1.com/lockbit-takedown-operation-cronos-a-long-awaited-psyops-against-ransomware/) — Analyst1
4. [LockBit Ransomware Takedown and Resurgence: Inside Operation Cronos](https://hivepro.com/blog/lockbit-takedown-and-resurgence/) — Hive Pro
5. [How Operation Cronos disrupted ransomware group LockBit](https://www.weforum.org/stories/2024/02/lockbit-ransomware-operation-cronos-cybercrime/) — World Economic Forum
6. [Takedown of the LockBit Ransomware Group: Global Takedown Cases 2024](https://improved-move.com/en/tutorial-category/takedowns/takedown-2024-global-cases/global-takedowns-2024-lockbit-operation-cronos/)
7. [LockBit Returns: Lessons Learned From Operation Cronos](https://www.picussecurity.com/resource/blog/lockbit-returns-lessons-learned-from-operation-cronos) — Picus Security
8. [Operation Cronos](https://arcticwolf.com/resources/blog/operation-cronos-the-takedown-of-lockbit-ransomware-group/) — Arctic Wolf
9. [The NCA announces the disruption of LockBit with Operation Cronos](https://www.nationalcrimeagency.gov.uk/the-nca-announces-the-disruption-of-lockbit-with-operation-cronos) — National Crime Agency (UK)
10. [Takedown Attempt and Resilience of Lockbit](https://www.menlosecurity.com/blog/takedown-attempt-and-resilience-of-lockbit-insight-into-operation-cronos) — Menlo Security
11. [#StopRansomware: LockBit 3.0 Ransomware Affiliates Exploit CVE 2023-4966 Citrix Bleed Vulnerability](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-325a) — CISA
12. [#StopRansomware: LockBit 3.0](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-075a) — CISA/FBI/MS-ISAC
13. [Understanding Ransomware Threat Actors: LockBit](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-165a) — CISA
14. [CISA, FBI, MS-ISAC Issue LockBit 3.0 Ransomware Advisory](https://www.govtech.com/security/cisa-fbi-ms-isac-issue-lockbit-3-0-ransomware-advisory) — GovTech

## Corrections Log

- None yet.
