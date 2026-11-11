# Magic Chess: Go Go — IL2CPP Dump

An IL2CPP metadata dump for **Magic Chess: Go Go** (`com.mobilechess.gp`), Unity **2019.4.33f1**.

The game ships a zero-byte `global-metadata.dat` and a stub `libil2cpp.so`, so a static dump gets
you nothing — this was captured from a running client. Published here as a reference for research
and interoperability work.

| | |
|---|---|
| Package | `com.mobilechess.gp` |
| Unity | 2019.4.33f1 |
| Backend | IL2CPP |
| Assemblies | 62 |
| Types | 26,443 |
| `Assembly-CSharp` | 19,382 types |
| Captured | November 2026 |

## What's in here

```
dump/mc_dump.cs        full dump, Il2CppDumper-style (~29 MB)
```

## Reading the dump

It's plain text, so `grep` is your friend:

```bash
# find a class
grep -n "class MCLogicHeroShop " dump/mc_dump.cs

# list every assembly and its type count
grep "^// ===== Assembly:" dump/mc_dump.cs
```

A couple of things to keep in mind:

- The `// 0x...` after a **field** is its offset from the object base. Those are stable for this build.
- The `// 0x...` after a **method** is an absolute, ASLR'd address from the process it was captured
  in — it is **not** an RVA. Rebase against your own `libil2cpp.so` load base if you need offsets.
- Gameplay logic that rides on **HybridCLR** hot-update DLLs isn't in here — those assemblies are
  loaded and interpreted separately, so this dump of the AOT image won't see them.

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, build on it; just keep the copyright line.

The license covers what I wrote. The dump itself is a factual description of a third-party binary
(class names, field offsets, method signatures). It isn't my work to "own," and it obviously isn't
licensed by the game's authors either — it's published here for research, interoperability and
education.

## Disclaimer

Not affiliated with, endorsed by, or connected to Moonton / Shanghai Moonton Technology. "Magic
Chess: Go Go" and "Mobile Legends" are their trademarks. Nothing here contains game assets, art,
or server code — only structural information recovered from the client binary. Respect the game's
terms of service and your local laws. Provided as-is, no warranty.
