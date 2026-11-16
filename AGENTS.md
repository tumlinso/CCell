# Working on CCell

CCell owns a C++20 reference biology package, its scientific methods, and
biological data integration. AnnData++ is CCell's data and IO component,
maintained as an independent Git submodule under src/io/anndatapp. Velocity++
remains a standalone Git submodule under external/velocitypp; preprocessing is
local CCell source under src/preprocess.

Cellerator is a sibling computation substrate. CCell owns integration of its
scientific methods with that substrate; future accelerated implementations may
use it explicitly. Keep the standard computational reference independent of
Cellerator. This checkout does not yet provide an acceleration component.

Read [coding_style.md](coding_style.md) before numerical design, implementation,
or review. It is binding authority: do not weaken, replace, move, or remove it,
or its protection here, without explicit user authorization. The standard
reference allocates nothing; callers supply all outputs, preparation, and scratch.
Consumer replacements may allocate explicitly. Shipped source and examples use
minimal scalar headers and compiler builtins, without STL machinery.

Public imports are `ccell`, `ccell.anndata`, `ccell.preprocess`, and
`ccell.velocity`. Re-export the existing component modules and preserve
their type identity. AnnData++ owns arrays, views, layouts, and lifetimes;
keep numerical operations native and memory/allocation behavior explicit.
Keep implementation-only changes out of public module interfaces.

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
