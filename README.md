# Hierarchical Chains · 分层链路

Research code for a RoboCasa system with five computation chains and C4–C12 components.

## Source code

Download [ALL_CODE_SNAPSHOTS.zip](ALL_CODE_SNAPSHOTS.zip) for **all 5500 locally archived source/configuration/asset/patch files**, including **43 frozen or isolated code snapshots**. The ZIP preserves the original directory structure and exact source bytes.

[SOURCE_MANIFEST.json](SOURCE_MANIFEST.json) lists every archived path, byte count and SHA-256. The ZIP SHA-256 is `eb37eab3a2a36ff05f1993ddbb4df142b4a5c5675813eb713c17f7d1ded2730f`.

```bash
unzip ALL_CODE_SNAPSHOTS.zip -d hierarchical-chains-source
cd hierarchical-chains-source/code/r49
```

The current runtime version is **R49**. **R50 qualification staging is experimental and has no reference application deployed.** Independent current-candidate qualification Q and the explicit application transaction remain unimplemented.

## Five computation chains

| Chain | Actual component flow |
|---|---|
| Preparation | C11 selection → C12 contract → C6 field preparation → P7 initialization → C8 readout → C10 |
| Reflex | Current observation and authorized bounds → C9 → C10 |
| Feedback | C5 → C8 fast scalar adjustment; or C5 → C7 → affected C6/C8 → C10 |
| Geometry update | C4 changed keys → contract dependencies/permissions → affected C6/C8 → C10 |
| Failure reselection | Actual failure → runtime cleanup → original C11 model → preparation |

## Module map

Under `code/r49/five_chains/`:

| Module | Responsibility |
|---|---|
| `components/c04_state.py` | WorldState, geometry changes and coordinate frames |
| `components/c05_feedback.py` | Event edges and continuous feedback |
| `components/c06_fieldprep.py` | P6 preparation and reuse |
| `components/c07_phase.py` | P7 phase state machine |
| `components/c08_readout.py` | Typed, unit-aware physical parameter readout |
| `components/c09_reflex.py` | Bounded reflex proposals |
| `components/c10_executor.py` | Arbitration, reference generation, sole `env.step` entry |
| `components/c11_selector.py` | Original neural selector adapters and structured-call validation |
| `components/c12_contract.py` | Eight skill templates, dependencies, write permissions and termination |
| `skills/recipes.py` | Explicit geometric parameter computations |
| `skills/live_grasps.py` | Current-asset grasp proposals, private pad checks and reduced gravity ranking |
| `envs/pose_ik.py`, `envs/scene_path.py` | IK, sampled full-scene paths and bounded measured-stall refresh |
| `envs/robocasa_adapter.py`, `envs/multitask_adapter.py` | Native observations, control interfaces and task predicates |
| `runtime.py`, `types.py`, `trace.py` | State lifecycle, interfaces and audit traces |

Newest isolated additions in `code/r50_qualification_staging/five_chains/envs/`: `reference_admission.py`, `reference_bridge.py`, `native_reference_preview.py`, `forecast_dependencies.py`, and `candidate_qualification.py`.

## Evidence status

- Frozen R12 independent evaluation: **4/20**, HeatMug 2/4 and PrepareCoffee 2/4; Steam/Bread/Pan 0/4 each.
- Historical native end-to-end successes exist for HeatMug, Coffee and Steam across versions. This is not a current-version 3/5 success rate.
- Frozen R46 known Steam configuration: 6000-step failure followed by 5717- and 5907-step successes. Recorded close-phase joint-bound violations remain unresolved.
- Bread R49 and Pan R48 remain complete-task failures.
- Latest existing R50 staging logs: 549 tests passed and mypy passed for 42 source files. This is not full deployed native-control validation.
- Geometry uses simulator ground truth; simulator contact forces are not independent tactile sensing. No real-robot or continuous-safety claim.

## Dependencies and reproduction

The archived files reference the original RoboCasa 1.0.1, Robosuite 1.5.2, MuJoCo 3.3.1 environments, robot assets, original selector adapter and official pretrained GraspGen dependencies. External environments and model weights are not included. Historical absolute paths require configuration for another machine. Standalone diagnostic scripts also require their registered evidence inputs from the separately retained local evidence package.

This repository publishes code. The large native trajectories and full experiment-log package are retained separately. No new experiment, training, model-weight change or control deployment was performed for this upload.

Snapshot directories: r12, r14, r15, r16, r17, r18, r19, r20, r21, r22, r23, r24, r25, r26, r27, r28, r29, r30, r31, r32, r33, r34, r35, r36, r37, r38, r39, r40, r41, r42, r43, r44, r45, r46, r47, r48, r49, r50_bridge_staging, r50_dependency_staging, r50_lifecycle_staging, r50_native_source_staging, r50_preview_staging, r50_qualification_staging.

Third-party dependencies retain their original licenses. No new project license is assigned by this upload.
