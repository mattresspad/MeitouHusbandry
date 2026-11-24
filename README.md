> **Archived: future development is moving to [AnimalBehaviors](https://github.com/Meitou-Modding-Ecosystem/AnimalBehaviors).** This repository preserves the Meitou v0.22.1 hitching-post playtest. Existing MeitouHusbandry packs and saves are not automatically compatible with AnimalBehaviors; migration remains pending.

# Meitou Husbandry

[Download the playtest](https://github.com/Meitou-Modding-Ecosystem/MeitouHusbandry/releases/tag/v0.1.0-playtest.2) · [Make a hitching post for my town](AUTHORING.md) · [Results](RESULTS.md) · [Feedback](https://github.com/Meitou-Modding-Ecosystem/MeitouHusbandry/issues)

An optional framework for animal interactions in Meitou. This first playtest gives a town author a hitching post: assign one owned animal, let it obey a direct movement order, and have it return when idle. Release it to end the assignment.

The framework adds no buildings by itself. **Stoat Hitching Post** is a separate data-only example. Transport, a dialogue framework and Maestro are not player dependencies.

## Install the example

Use **MeitouClient v0.22.1, Windows x64**, and your own Kenshi installation. Download both mod ZIPs from the release and extract their enclosing folders into `Kenshi/mods`. Enable this order:

1. **Meitou Husbandry**
2. **Stoat Hitching Post**

Allow the framework's code mod in Meitou when prompted. The sample post stands outside Stoat at **X 35071, Z -70668**. Select a conscious squad animal beside it and use **F10 → Assign to nearby hitching post**. A second animal cannot take an occupied post. Give the assigned animal a move order outside the radius; once idle it returns. Use **F10 → Release from hitching post**, including during its return.

Assignments survive saving and reloading. Blocked routes stop retrying and report a diagnostic; clear the obstruction, release and assign again. Existing jobs, combat and player orders retain priority. The tester kit includes two-Garru fixture saves and a short walkthrough.

## Make a hitching post for my town

Your mod owns the building, its appearance and collision, each physical placement, and `husbandry.json`. Husbandry supplies assignment, return behavior and persistence. See the [editable Stoat project](projects/Stoat%20Hitching%20Post/) and [authoring recipe](AUTHORING.md).

The framework ships an **Add hitching post** descriptor for [Maestro v0.1.0-playtest.1](https://github.com/Meitou-Modding-Ecosystem/MeitouMaestro/releases/tag/v0.1.0-playtest.1). That editor requires **v0.20.1 game readers** for authoring; the resulting pack is tested here on **v0.22.1**. Players do not need the editor or older readers. Authors may also create the same dependency and JSON directly.

Other code mods can query the current world's assignment through `IHusbandryApi.GetHitch`. [Consumer example](AUTHORING.md#read-an-assignment-from-another-framework).

## Build and contribute

Use PowerShell 7 and .NET SDK **11.0.100**. Set `MEITOU_DIR` to the extracted official v0.22.1 Windows game folder containing `MeitouClient.dll`. Set `KENSHI_PATH` to your own Kenshi installation for asset-dependent checks.

```powershell
./tools/package.ps1
dotnet run --project tests -c Release
dotnet build qa/Live -c Release
```

The mod archives are written to `dist/`. [Repeat the live checks](qa/README.md) · [Contributing](CONTRIBUTING.md) · [Licensing](LICENSING.md).

Framework software and tools are **GPL-3.0-or-later**. Original sample definitions and guides are **CC0-1.0**. No Kenshi art or game DLLs are included.
