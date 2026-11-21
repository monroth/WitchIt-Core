# Witch It+ core

The base libraries of Witch It+ mods, a mod source for the [Witch It+ launcher](https://github.com/monroth/WitchIt-Plus).
Every mod needs Core; the others are there for any mod that shows menus and rules, edits a map in Creative or keeps
its data in a map. The launcher installs them with the mods that need them.
`witchit-mods.json` lists them and their versions; each version is a release `<id>-v<version>`.

## Libraries

| Library | What it does |
|---|---|
| Core | The runtime, its native part and the updater: hooks, the session, data between the host and its guests, joining and hosting with the right mods. Everything needs it. |
| UIKit | The mods' menus, settings and shortcuts, in the game's own look. |
| Map markers | Markers placed in Creative and kept in the map: a mod adds its own kinds of objects to a map. |
| WorldKit | What every Creative tool shares: the selection, one undo, clicks in the level, marks over the level. |

The mods built on them: [WitchIt-Modpack](https://github.com/monroth/WitchIt-Modpack).

## Making your own source

A source is a public GitHub repository (or a private one, with a read-only token) with
`witchit-mods.json` in its root:

```json
{"mods": {"my-mod": {
  "name": "My Mod",
  "description": "One sentence.",
  "tags": ["gameplay", "host"],
  "sync": false,
  "folders": ["MyMod"],
  "versions": {
    "1.0.0": {"sha256": "<sha256 of my-mod.zip>",
              "needs": {"monroth/WitchIt-Core:core": ">=0.4"}}
  }}}}
```

- **Archive:** `my-mod.zip`, paths starting at `ue4ss/` (`ue4ss/Mods/MyMod/manifest.lua`, …), only
  inside the mod's own `folders`.
- **Release:** tag `my-mod-v1.0.0`, asset `my-mod.zip`; its sha256 in the index.
- **Versions:** `N.N.N` are releases; `N.N.N-nightly.<number>` nightlies; anything else an alpha
  (chosen only by hand).
- **Needs:** `id` (same source) or `owner/repo:id`; conditions `1.2.0`, `1.2.*`, `>=1.0`,
  `<=1.*`, space-separated.
- **Tags:** what it is — `gameplay`, `maps`, `creative`, `utility`, `technical` (a library); where
  it runs — `host`, `client`. `sync: true` means every player in a match needs the host's version.
- **Your mod's code:** see [the mod guide](PUBLISHING-MODS.md) (manifest, package, runtime).

Players add `your-name/your-repo` on the launcher's **Sources** page.

You can use this repository (or [WitchIt-Modpack](https://github.com/monroth/WitchIt-Modpack)) as an example of a source with a correct `witchit-mods.json` and releases.

## Source

The source of these libraries is in [`source/`](source). They are built with our UE4SS: [monroth/RE-UE4SS-Witchit@ebae54ca](https://github.com/monroth/RE-UE4SS-Witchit/tree/ebae54ca938e36ee1a898d11b66149489dbfb670).
