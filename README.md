# Windows Server 2026 VPS: How Cheap Is Too Cheap, Which Evoxt Plan Fits Your Workload, and Is the Licence Actually Included? (Full Plan Table)

Evoxt lists Windows Server 2022 VPS from $2.99 a month, but that tier has 512 MB of RAM, which is not enough to run the operating system. The first plan that runs Windows properly is **VM-1 at $5.99** (1 vCPU, 2 GB RAM, 20 GB storage), and the one most buyers keep is **VM-2 at $11.99** (2 vCPU, 4 GB RAM, 30 GB). Windows licensing is bundled into those prices rather than added as a separate line at checkout.

What follows: every plan on Evoxt's Windows page with current pricing, the three licence models you will run into in this market and what each one means the week activation expires, sizing rules by workload, and the cases where Cloudzy, Xaro or ColossusCloud are the better buy.

> **Most readers should take VM-2 at $11.99/month.** It is the smallest tier where an RDP session, a browser and a background service can share the box without swapping. Take VM-1 ($5.99) only if the server has one light role and you are not going to browse from it. 👉 [See Evoxt's Windows Server 2022 plans and current pricing](https://bit.ly/EvoXt)

## Every Evoxt Windows plan, priced

Evoxt is a Malaysian provider that has been selling since 2020 and prices on CPU clock speed (3.5 GHz and up, with faster nodes on newer hardware) rather than on core count alone. The Windows lineup below is what its Windows VPS page shows today, in USD, billed monthly.

| Plan | vCPU · RAM | Storage | Price | Order |
| --- | --- | --- | --- | --- |
| VM-0.5 | 1 vCPU · 512 MB | 5 GB | $2.99/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-0.75 | 1 vCPU · 1 GB | 10 GB | $4.99/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-1 | 1 vCPU · 2 GB | 20 GB | $5.99/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-1.5 | 2 vCPU · 2 GB | 20 GB | $6.95/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-2 | 2 vCPU · 4 GB | 30 GB | $11.99/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-3 | 4 vCPU · 4 GB | 30 GB | $14.99/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-4 | 4 vCPU · 8 GB | 60 GB | $23.99/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-6 | 8 vCPU · 8 GB | 60 GB | $29.99/mo | [ Deploy](https://bit.ly/EvoXt) |
| VM-8 | 8 vCPU · 16 GB | 80 GB | $47.99/mo | [ Deploy](https://bit.ly/EvoXt) |

Above VM-8 the console shows larger configurations; price those directly there if 16 cores is your floor.

The column to stare at is storage, not RAM. Windows Server 2022 with the desktop experience consumes a large share of a 20 GB disk before you install a single application, which leaves VM-1 very little room for Windows Update, the page file and the service you actually bought the server for. If the box will hold data or logs, start at VM-2's 30 GB or VM-4's 60 GB.

**What every plan includes, regardless of tier:**

| Feature | Detail |
| --- | --- |
| Virtualisation | KVM, full isolation rather than a container-based VPS |
| Backups | Weekly offsite backup, included at no cost |
| Panel firewall | Layer 3 rules applied from the web console, before you ever open RDP |
| VNC console | Browser access when RDP is wedged |
| Cloning and sub-accounts | Duplicate a configured VM; role-scoped logins for admin, billing, support |
| API | `api.evoxt.com` for automated deploys and management |
| IP management | Swap IPs between VMs, order floating IPs for failover |
| Rescue mode | One-click boot into recovery for a broken boot config |
| Billing terms | Monthly, quarterly, or prepaid up to three years. No hourly billing |
| Not included | DDoS protection (sold separately), reverse DNS, hourly spin-up |

## The licence question nobody puts in the headline

Windows licensing is where cheap Windows VPS offers diverge most, and it is almost never in the price banner. Three models circulate:

1. **Genuine licence under a Microsoft SPLA agreement.** ColossusCloud states it is an SPLA partner and that every Windows Server 2022 VPS ships with a compliant licence, with Office and SQL Server as paid add-ons.
2. **Trial licence or BYOL.** Cloudzy ships a trial licence so the server is usable immediately, and lets you bring your own key and activate it yourself.
3. **Evaluation image with no licence at all.** Some hosts install Microsoft's evaluation build and leave activation to you. When the evaluation period ends, the server shuts itself down on a timer until a key is applied. That is a production outage with a calendar date attached.

Evoxt sells its Windows plans with Windows as the operating system at the listed price, and its stated position is that licensing is bundled rather than invoiced separately. That is the model you want. Two details are still worth getting in writing before you pay, because they are the two that bite later: whether the image activates permanently after deployment or runs against a trial clock, and whether the licence stays valid if you upgrade the plan mid-term.

The licence cost is also the reason a $2.99 Windows VPS is a red flag rather than a bargain. A 512 MB VM will not run Server 2022, and a Windows price that undercuts Linux by a wide margin usually means the licence is not in the price.

👉 [Check the Windows image and licence terms in Evoxt's console before paying](https://bit.ly/EvoXt)

## What Server 2022 actually gives you, and how long it lasts

Three differences from older releases matter on a rented box:

**TLS 1.3 is on by default** for HTTP.sys and Schannel, with weaker cipher suites disabled out of the box. For an IIS or ASP.NET site that means modern encryption without registry edits after deployment.

**Secured-core server** combines hardware-rooted trust with virtualization-based security and Credential Guard, so credentials in memory are harder to extract through a kernel-level attack. On a VPS this depends on the host exposing a virtual TPM; ask before you assume you get it.

**SMB encryption supports AES-256-GCM and AES-256-CCM**, which covers file transfers between servers without bolting on IPsec. Relevant if the VM mounts a share from another machine or replicates to one.

On lifecycle, the dates hosting providers publish are mainstream support through **October 2026** and extended support through **October 2031**. Mainstream support has now ended, so 2022 sits in the security-patch phase: fixes yes, new features no. It remains the LTSC release most application vendors certify against, and it shares its kernel with Windows 11, so .NET and Win32 software runs unmodified. Treat it as the safe target for an existing stack, and price Server 2025 separately if you are starting fresh on a current .NET version.

## Which plan fits which job

**One IIS site with a small database.** VM-2 at $11.99. Four gigabytes covers IIS worker processes, SQL Server Express and the OS with headroom. VM-1 works if the site is mostly static and you rotate logs aggressively, but 20 GB is a real constraint once IIS logs and Windows Update start accumulating.

**Multi-user RDP.** Budget roughly 1.5 to 2 GB per concurrent user, plus 2 GB for the OS. One or two light users fit VM-2; three to four users need VM-4 at $23.99 (8 GB, 4 vCPU); five or more pushes you to VM-8 at $47.99 (16 GB, 8 vCPU). Office plus a browser is the memory hog here, not the desktop itself.

**A domain controller.** A small AD DS forest runs comfortably in 2 GB, so VM-1 at $5.99 is enough. Buy two of them for a second DC rather than one larger box: two VM-1s cost $11.98, less than a single VM-4, and you get redundancy instead of a bigger single point of failure.

**SQL Server.** Sizing is memory-bound. VM-4 at $23.99 (8 GB) is the realistic floor for anything production; go to VM-8 at $47.99 once the working set climbs past about 5 GB. Putting a database on VM-1 is possible and unpleasant.

**Windows containers.** Core count matters more than RAM here, so VM-3 at $14.99 (4 vCPU, 4 GB) or VM-6 at $29.99 (8 vCPU, 8 GB). Watch the disk: Windows base images are measured in gigabytes, and 30 GB disappears quickly.

👉 [Price the VM-2 and VM-4 configurations side by side](https://bit.ly/EvoXt)

## Where Evoxt is not the answer

Evoxt wins on price per gigabyte of RAM at the low end, and on bundling the licence without an extra line item. It loses on storage density, refund policy visibility and network extras.

| Provider | Windows entry point | Notable extras | Where it wins |
| --- | --- | --- | --- |
| Evoxt | $5.99 (1 vCPU, 2 GB, 20 GB) | Licence bundled, weekly offsite backup, KVM | Cheapest 4 GB tier at $11.99 |
| Xaro | $7.00 (1 vCPU, 2 GB, 25 GB, licence included) | Four tiers up to 16 GB / $36 | More disk per dollar at 4 GB: $10 for 45 GB |
| Cloudzy | $14.48 listed (2 vCPU, 4 GB DDR5, 120 GB NVMe) | 13 regions, 60-second provisioning, 14-day money-back, trial licence or BYOL, Trustpilot 4.5/5 from 719 reviews | Storage, uplink speed, refund window, region choice |
| ColossusCloud | Not listed in our check | SPLA genuine licence, 6 data centres, Ceph three-copy storage, deployment under 5 minutes | Licence paperwork and storage redundancy |

Three concrete cases where you should not buy from Evoxt. You need a refund guarantee: Cloudzy publishes a 14-day, no-questions money-back policy, and Evoxt does not advertise one, so confirm the cancellation terms first. You need more than 80 GB of disk on a single VM without jumping tiers. You need hourly billing for ephemeral work, which Evoxt does not offer at all; its terms are monthly, quarterly or prepaid up to three years. Reverse DNS is also excluded, which kills the plan if the VM will send mail.

Evoxt's regional coverage is broad rather than deep: 16 locations across North America, Europe and Asia-Pacific, with premium network routes into Hong Kong, Osaka and Malaysia for lower APAC latency. If your users sit somewhere not on that list, latency will decide the purchase for you.

## The first 30 minutes after deployment

1. Run Windows Update and reboot until it reports clean.
2. Close RDP to the world. Use the panel's Layer 3 firewall to allow 3389 only from your own addresses, or put RDP behind a VPN.
3. Set unique passwords for every account, enable Network Level Authentication, and remove roles and features you are not using.
4. Install what you came for: IIS and .NET, SQL Server, the DNS role.
5. Confirm the weekly offsite backup actually ran, then add basic monitoring.
6. Sort out reverse DNS before you send any mail from the box; it is not part of the plan.

## The decision, in one paragraph

Single IIS site or a light admin box: **VM-2, $11.99**. Multi-user RDP for a small team, or a production SQL Server: **VM-4, $23.99**. A domain controller: **two VM-1s at $11.98 combined**. Container hosts: **VM-3 or VM-6**, depending on how many cores your build pipeline eats.

Before you pay, get two things confirmed: what the Windows licence actually is (bundled activation, trial, or bring-your-own), and the price of the term that follows your first one. Evoxt's plan page does not break out a separate renewal rate for these tiers, and the three-year prepay option is exactly where a price change would be hardest to notice.

👉 [Start with VM-2 on Evoxt's deploy console](https://bit.ly/EvoXt)
