# The Death of the Man-Month

**Fifty years after Brooks — how AI turns one mind into a team.**

A talk by Glenn West. Forty years of systems engineering, two years of managing machine minds, and the code to show for it.

📺 **Watch:** *(video coming soon)*

---

## The talk in one paragraph

In 1975, Fred Brooks wrote *The Mythical Man-Month*: adding people to a late software project makes it later, because communication paths grow as n(n−1)/2. His prescription — the surgical team, one chief programmer amplified by everyone else — never worked, because the amplifiers were also people. AI agents are that surgical team with the communication tax deleted. They don't meet, they don't defend turf (mostly — see the talk), and they multiply whatever mind holds the design. The evidence: one engineer, in spare time, built a complete datacenter operating system in Rust — and then, as a deliberate "pick something impossible" test, a full BGP-based software-defined network, the kind of system industry estimates put at 700–1,200 person-years for comparable commercial stacks.

## The numbers

The whole stormcos stack, measured from the repositories themselves (`git ls-files`, shipped code only — no tests, tooling, or vendored code; snapshot 2026-10-07). The full measurement — every repo, every count, and the `measure.py` that produced it — is public: **[mythical-man-month-2026](https://github.com/glennswest/mythical-man-month-2026)**.

| The stack | Number |
|---|---|
| Repositories | **54** |
| Lines of shipped code (96.2% Rust) | **559,317** |
| Issues — every piece of work starts as one; issues drive the system | **3,923** |
| Human attention, at one minute per issue (read, answer or approve) | **≈ 65 hours** |
| Shipped lines per human hour | **≈ 8,554** |
| Calendar span (about 17 minutes of attention a day — weekends, early mornings, after hours) | **232 days** |

| Highlights | Number |
|---|---|
| NextNFS, v0.1.0 → v0.13.8 — a full NFSv4 server in Rust | **11 days** |
| Passing tests on that release | **591** |
| Updating a running node (golden-image clone swap, not an install) | **2 seconds** |
| flowsdn — BGP software-defined networking: 354 issues, ~6 hours of attention | **31 days** |
| Industry scale for comparable commercial SDN stacks | **700–1,200 person-years** |

## The evidence — start here

Seven repos, one per claim in the talk:

| Repo | What it proves |
|---|---|
| [flowsdn](https://github.com/glennswest/flowsdn) | The "impossible" one: a full BGP-based software-defined network in Rust — benchmarked, tested, meeting performance goals |
| [stormbootx](https://github.com/glennswest/stormbootx) | UEFI NVMe/TCP boot with no kernel, no initramfs, no PXE — home of the device-drivers-in-an-hour story |
| [stormblock](https://github.com/glennswest/stormblock) | Pure-Rust enterprise block storage — NVMe-oF/TCP + iSCSI targets with software RAID |
| [rustkube](https://github.com/glennswest/rustkube) | Kubernetes-API-compatible container orchestrator in Rust |
| [fastetcd](https://github.com/glennswest/fastetcd) | Wire-compatible etcd v3 replacement — multi-node Raft |
| [nextnfs](https://github.com/glennswest/nextnfs) | NFSv4.0/4.1/4.2 server in Rust — v0.1.0 to v0.13.8 in 11 days, 591 passing tests |
| [zeroboot](https://github.com/glennswest/zeroboot) | Sub-millisecond VM sandboxes via copy-on-write forking — zero install time, zero recovery time |

## "Go forth and multiply" — the drivers

The talk tells the story of device drivers going from a lost quarter to an hour. Here are the receipts: eight UEFI network drivers in `no_std` Rust, each loaded by stormbootx, written after the first one worked and the agent kept volunteering for more hardware.

| Driver | Hardware |
|---|---|
| [stormnic-e1000e](https://github.com/glennswest/stormnic-e1000e) | Intel e1000e (82574L, 82579, I217–I219) |
| [stormnic-igb](https://github.com/glennswest/stormnic-igb) | Intel igb (i350, i210/i211, 82576/82580) |
| [stormnic-ixgbe](https://github.com/glennswest/stormnic-ixgbe) | Intel 82599/X540/X552 10G |
| [stormnic-i40e](https://github.com/glennswest/stormnic-i40e) | Intel i40e (X710, XL710, XXV710, X722) |
| [stormnic-mlx4](https://github.com/glennswest/stormnic-mlx4) | Mellanox ConnectX-3 |
| [stormnic-mlx5](https://github.com/glennswest/stormnic-mlx5) | Mellanox mlx5 (ConnectX-4/4 Lx/5/6) |
| [stormnic-realtek](https://github.com/glennswest/stormnic-realtek) | Realtek RTL8111/8168, RTL8125, RTL8126 |
| [stormnic-virtio](https://github.com/glennswest/stormnic-virtio) | virtio-net (modern, virtio 1.x) |

## The Storm family — public index

The talk's "one architect, fifty components" wall. The public members (parts of the stack are still private while they stabilize — they open up as they harden):

| Repo | One-liner |
|---|---|
| [stormagents](https://github.com/glennswest/stormagents) | Sub-millisecond VM sandboxes for AI agents via copy-on-write forking |
| [stormblock](https://github.com/glennswest/stormblock) | Pure-Rust block storage engine — NVMe-oF/TCP + iSCSI targets, software RAID |
| [stormbootx](https://github.com/glennswest/stormbootx) | UEFI NVMe/TCP boot extension — no kernel, no initramfs, no PXE |
| [stormconsole](https://github.com/glennswest/stormconsole) | StormCOS web console — pluggable, OpenShift-style, built on stormd and stormview |
| [stormcoredns](https://github.com/glennswest/stormcoredns) | CoreDNS reimplemented in Rust — Corefile, plugin chain, full plugin set |
| [stormcos_builder](https://github.com/glennswest/stormcos_builder) | Builds stormcos boot images on component change; provisions single-node clusters on demand |
| [stormcos_qa](https://github.com/glennswest/stormcos_qa) | QA: test standard, auto-filing runner, must-gather; tombstones failed images |
| [stormlb](https://github.com/glennswest/stormlb) | API/ingress VIP load balancer — health-checked L4 + VRRP / BGP-anycast |
| [stormrfb](https://github.com/glennswest/stormrfb) | RFB (RFC 6143) in Rust — sans-I/O codec, client and server |
| [stormstar](https://github.com/glennswest/stormstar) | Lightweight RPM content management — single Rust binary for edge |
| [stormview](https://github.com/glennswest/stormview) | Shared Svelte UI component library — and yes, it is a library *only* (watch the talk) |

Plus the wider stack: [microdns](https://github.com/glennswest/microdns) (Rust DNS / DHCP / IPAM with REST API), [mkube](https://github.com/glennswest/mkube) (virtual Kubernetes for MikroTik routers), and the rest of the catalog.

**Full catalog — 500+ public repos:** https://github.com/glennswest

## Who

Glenn West — Principal Software Engineer. Forty-plus years spanning telecom, semiconductor, aerospace, and cloud: FPGA hardware-as-code in the 1980s, carrier-grade telco products in the 1990s, cloud strategy across APAC, and field engineering for strategic telco and cloud accounts today.

Contact: gwest@redhat.com · glenn_west@hotmail.com · [LinkedIn](https://www.linkedin.com/in/glenn-west-664a58)
