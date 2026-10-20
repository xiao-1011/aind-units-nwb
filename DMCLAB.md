# DMC lab fork of aind-units-nwb

Lab-maintained NWB units step for the AIND ephys pipeline on Arrhenius.
The capsule layout (`code/run`, `code/run_capsule.py`) is unchanged so the stock
pipeline can run it through its repo/commit override:

```
nwb_units_repo   = 'https://github.com/xiao-1011/aind-units-nwb'
nwb_units_commit = '<full commit hash>'
```

Always pin the full commit hash in the pipeline config. Tags are for people.

## Branches

| Branch | Content |
|---|---|
| `main` | Mirror of `AllenNeuralDynamics/aind-units-nwb` `main`. Never commit here. |
| `dmclab` | Our changes, as a short series of commits on top of an upstream release commit. |

No other branches are kept. Upstream development branches live upstream.

## Production tags

| Tag | Commit | Upstream base | Used by |
|---|---|---|---|
| `dmclab-1.4.0-v2` | `cdf8be6` | `c7cfa6c` (pipeline 1.4.0) | DREDGE-100 v1 (`batch_runs/20261006_180017`) and v2 (`batch_runs/20261012_125513`) |

Tags are never moved or deleted: archived runs refer to these commits. The pipeline
clones this fork and checks out the pinned hash, so the commit must stay reachable
from a branch or tag of this repository (an upstream PR ref is not enough).

## Changes relative to upstream

1. `cdf8be6` Derive NWB electrode group labels from the recording names
   (`..._group<N>`) instead of the channel `group` property. With SpikeInterface
   0.105.0, slicing re-enumerates `group` from 0, so every shank of a multi-shank
   probe was labelled `<probe>_group0` and shank 1 failed with `KeyError`.

Fixed upstream in SpikeInterface by PR #4838 (SI >= 0.105.1). Pipeline 1.4.1 ships
SI 0.105.2 and stock aind-units-nwb `67e2538`, so this fork is no longer needed
after migrating to 1.4.1. Upstream PR #32 was closed for that reason.

## Retirement

After production moves to pipeline >= 1.4.1 and the `nwb_units_repo/commit`
override is removed, archive this repository (read-only) instead of deleting it,
so v1/v2 stay reproducible from their pinned configs.
