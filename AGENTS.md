# Working on CCell

CCell owns a C++20 reference biology package, its scientific methods, and
biological data integration. AnnData++ is CCell's data and IO component,
maintained as an independent Git submodule under src/io/anndatapp. Velocity++
remains a standalone Git submodule under external/velocitypp; preprocessing is
local CCell source under src/preprocess.

Cellerator is the reusable computation substrate and an approved normal
dependency for CCell objects, interfaces, and implementations. CCell owns its
scientific methods and their integration with that substrate. Compose its
public owners, buffers, views, layouts, and prepared operations; keep reusable
computational machinery in Cellerator. Approval of that dependency does not
claim that this checkout already links it or provides acceleration.

Read [coding_style.md](coding_style.md) before numerical design, implementation,
or review. It is binding authority: do not weaken, replace, move, or remove it,
or its protection here, without explicit user authorization. The standard
reference allocates nothing; callers supply all outputs, preparation, and scratch.
Explicit provisioning through Cellerator resource operations may allocate and
retain storage. Reuse sufficient capacity; repeated numerical execution must
allocate nothing, including metadata and ownership bookkeeping. Consumer
replacements expose their allocation and complete costs. All authored shipped
native code and examples use direct calculations, minimal scalar headers and
compiler builtins, without STL machinery. Cellerator public abstractions are
permitted under their own equally strict authority, not as a way to conceal
prohibited machinery in CCell helpers.

Public imports are `ccell`, `ccell.anndata`, `ccell.preprocess`, and
`ccell.velocity`. Re-export the existing component modules and preserve
their type identity. AnnData++ owns biological data/IO and its acquired array
descriptors; Cellerator owns reusable computation storage and execution types.
Preserve the lifetime and layout contract of each; do not duplicate generic
storage machinery in CCell. Keep numerical operations and costs explicit.
Keep implementation-only changes out of public module interfaces.

Run `python3 tools/check_native_style.py` and the registered checker fixtures
for changes to native source or its checker. Mechanical checks do not establish
compactness, indirect allocation, or unnecessary work: review the affected
calculation and helpers. Existing noncompliant code is not precedent; new and
reworked code must comply without making an unrelated repository-wide cleanup
a prerequisite. Preserve the parallel implementation work.

Use the debug preset with Clang 18, matching clang-scan-deps, CMake >=3.28,
and Ninja: configure, build, then run CTest. It checks composition through
the umbrella and individual module imports and through an installed package.
The same root build owns preprocessing's numerical tests and packaging; do
not recreate standalone preprocess build or package metadata. Its license
and third-party notices live at the repository root. Velocity++ numerical
changes also require its standalone checks. Historical qualification records
are not current-source evidence.

Preserve concurrent and unknown work, staged changes, submodule histories,
scientific fixtures, and historical receipts. Do not reset or clean work,
delete remote repositories, or rewrite workflow authority. Use configured
Codex subagents for useful independent work, with explicit file ownership;
keep intent, integration, and acceptance with the root.
