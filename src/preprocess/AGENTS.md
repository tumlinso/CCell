# Working on preprocess inside ccell

## Purpose and boundaries

The `preprocess` subtree is part of CCell's C++20 reference biology
package. Its public functions provide an explicit CPU reference built on
AnnData++. Scanpy supplies pinned numerical comparison behavior; it does not
dictate Python-style call semantics.
Numerical similarity is required; bitwise identity and universal equality of
intermediates are not requirements. Explain consequential differences and
qualify them with scientific quantities and tolerances.

The current CPU `preprocess` target depends on AnnData++ and has no runtime
Python, Scanpy, Torch, CUDA, or Cellerator dependency. Cellerator is an approved
normal dependency for CCell objects and implementations when used; the current
target wiring is not a prohibition. Keep scientific method contracts distinct
from reusable computation and explicit resource provisioning.

## C++ and numerical style

- Follow [the root numerical style](../../coding_style.md), STYLE.md, and the protected
  [Cellerator C++ coding style](/home/tumlinson/Cellerator/coding_style.md).
  Keep its reference unchanged.
- Use C++20 named modules and .cppm interfaces. Public consumption is
  import preprocess;. Do not require import std; or add a public umbrella
  header.
- Keep exported module interfaces and consumer recompilation small. Put
  implementation-only code in compiled source files.
- Use direct arrays, pointers, extents, strides, sparse offsets and indices.
  Make allocation, conversion, mutation, and materialization explicit.
- Reuse AnnData++ acquired data descriptors and Cellerator public computation
  objects where appropriate. Preserve their distinct shape/layout/lifetime
  contracts; do not maintain a parallel generic matrix or ownership framework.
  Preprocess owns numerical operations and their additional contracts.
- Numerical sizing, preparation and evaluation consume supplied storage.
  Explicit provisioning uses existing Cellerator resource operations. Reuse
  sufficient capacity; repeated calls and compatible smaller inputs allocate
  nothing. Cheap stack views need no caching framework.
- Resolve validation and representation dispatch at acquisition boundaries.
  Keep element loops free of type-erased dispatch, repeated validation and
  hidden synchronization. Callers own parallel execution.
- Keep numerical types and accumulation explicit. Preserve the operation's
  declared mathematical method and test against the pinned reference cases.

## Build and validation

Use Linux, Clang 18 with matching clang-scan-deps, CMake 3.28 or newer, and
Ninja 1.11 or newer.

The maintained source is `ccell/src/preprocess`. Build and validate it through the
root ccell CMake project as described in [the root README](../../README.md). It
has no standalone configure or package workflow. `CCELL_BUILD_TESTS` includes
the prefixed native suites and example; `CCELL_BUILD_QUALIFICATION` enables the
optional Scanpy comparison and native benchmark sources.

Optional Python interoperability is development-only. Its reference environment
pins Scanpy 1.11.5 and the packages in tests/preprocess/requirements-reference.txt.
See ../../docs/preprocess/development.md and ../../docs/preprocess/validation.md.

Performance probes should be bounded to 30 seconds and compare identical
workloads. Keep source and toolchain identity with results. Do not claim speed
or memory improvements from source inspection alone.

## Ownership and preservation

Preserve unknown work and supplied inputs. Do not reset or clean Git state,
force-push, replace authority data, or edit the sibling AnnData++ or Velocity++
components as part of preprocessing work. Keep generated builds, local
reference environments, data and raw reports out of Git.

The former `preprocess-cppm` GitHub repository and Project Control registration
describe historical standalone development. They do not establish current
ownership or workflow authority; the maintained source is `ccell/src/preprocess`.

Use the configured Codex agent profiles for useful independent work. Root
retains user intent, interface decisions, integration, and acceptance. Use
Codex subagents for engineering; preserve concurrent edits and never use
Project Control local coding workers as engineering delegates.
