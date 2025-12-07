# Scene Names Guide

## Scene Name Mappings by Environment Type

### 1. **GraspSingleOpenedCokeCanInScene-v0** (Pick Coke Can)
**Default:** `google_pick_coke_can_1_v4`

**Alternative scenes:**
- `Baked_sc1_staging_objaverse_cabinet1_h870`
- `Baked_sc1_staging_objaverse_cabinet2_h870`

**Example:**
```bash
--env-name GraspSingleOpenedCokeCanInScene-v0 --scene-name google_pick_coke_can_1_v4
```

---

### 2. **MoveNearGoogleBakedTexInScene-v0/v1** (Move Near)
**Default:** `google_pick_coke_can_1_v4`

**Alternative scenes:**
- `google_pick_coke_can_1_v4_alt_background`
- `google_pick_coke_can_1_v4_alt_background_2`
- `Baked_sc1_staging_objaverse_cabinet1_h870`
- `Baked_sc1_staging_objaverse_cabinet2_h870`

**Example:**
```bash
--env-name MoveNearGoogleBakedTexInScene-v1 --scene-name google_pick_coke_can_1_v4
```

---

### 3. **Drawer Environments** (Open/Close Drawer)
**Environments:**
- `OpenTopDrawerCustomInScene-v0`
- `OpenMiddleDrawerCustomInScene-v0`
- `OpenBottomDrawerCustomInScene-v0`
- `CloseTopDrawerCustomInScene-v0`
- `CloseMiddleDrawerCustomInScene-v0`
- `CloseBottomDrawerCustomInScene-v0`
- `PlaceIntoClosedTopDrawerCustomInScene-v0`
- `PlaceIntoClosedMiddleDrawerCustomInScene-v0`
- `PlaceIntoClosedBottomDrawerCustomInScene-v0`

**Default:** `frl_apartment_stage_simple`

**Alternative scenes:**
- `modern_bedroom_no_roof`
- `modern_office_no_roof`
- `dummy_drawer` (for visual matching)

**Note:** Drawer tasks typically require `--enable-raytracing` flag!

**Example:**
```bash
--env-name OpenTopDrawerCustomInScene-v0 --scene-name frl_apartment_stage_simple --enable-raytracing
```

---

### 4. **Bridge/WidowX Environments**
**Environments:**
- `PutCarrotOnPlateInScene-v0`
- `StackGreenCubeOnYellowCubeBakedTexInScene-v0`
- `PutSpoonOnTableClothInScene-v0`
- `PutEggplantInBasketScene-v0`

**Scenes:**
- `bridge_table_1_v1` (for most bridge tasks)
- `bridge_table_1_v2` (for `PutEggplantInBasketScene-v0`)

**Example:**
```bash
--env-name PutCarrotOnPlateInScene-v0 --scene-name bridge_table_1_v1
--env-name PutEggplantInBasketScene-v0 --scene-name bridge_table_1_v2
```

---

## How to Discover Available Scene Names

### Method 1: Check the Scripts
Look at the example scripts in the `scripts/` directory:
- `scripts/pick_coke_can_*.sh` - for pick coke can scenes
- `scripts/drawer_*.sh` - for drawer scenes
- `scripts/move_near_*.sh` - for move near scenes
- `scripts/bridge.sh` - for bridge scenes

### Method 2: Check ManiSkill2 Data Directory
Scene names correspond to directories/files in the ManiSkill2 data directory:
```bash
# Check if you have access to the ManiSkill2 data directory
ls $HOME/.cache/mani_skill2/scenes/  # or similar path
```

### Method 3: Try Running with Invalid Scene Name
If you use an invalid scene name, ManiSkill2 will raise an error that might list available options.

### Method 4: Check ManiSkill2 Documentation
Scene names are defined in ManiSkill2's scene registry. Check:
- ManiSkill2 repository documentation
- The `ManiSkill2_real2sim` submodule for custom scenes

### Method 5: Inspect Environment Source Code
Look at the environment implementation in:
```
ManiSkill2_real2sim/mani_skill2_real2sim/envs/custom_scenes/
```

---

## Quick Reference Table

| Environment Type | Default Scene | Alternative Scenes |
|-----------------|---------------|-------------------|
| Pick Coke Can | `google_pick_coke_can_1_v4` | `Baked_sc1_staging_objaverse_cabinet1_h870`, `Baked_sc1_staging_objaverse_cabinet2_h870` |
| Move Near | `google_pick_coke_can_1_v4` | `google_pick_coke_can_1_v4_alt_background`, `google_pick_coke_can_1_v4_alt_background_2` |
| Drawer (Open/Close) | `frl_apartment_stage_simple` | `modern_bedroom_no_roof`, `modern_office_no_roof`, `dummy_drawer` |
| Bridge Tasks | `bridge_table_1_v1` | `bridge_table_1_v2` (for eggplant task) |

---

## Notes

1. **Default Scene:** If you don't specify `--scene-name`, it defaults to `google_pick_coke_can_1_v4` (as defined in `simpler_env/evaluation/argparse.py`)

2. **Scene Compatibility:** Not all scenes work with all environments. The scene must be compatible with the environment's requirements (e.g., drawer scenes need cabinets).

3. **Visual Matching:** Some scenes are specifically designed for visual matching evaluation (e.g., `dummy_drawer`).

4. **Ray Tracing:** Drawer environments typically require `--enable-raytracing` for proper depth perception.

