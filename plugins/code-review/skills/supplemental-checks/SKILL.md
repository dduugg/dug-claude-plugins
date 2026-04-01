# Supplemental Code Review Checks

These are additional checks to apply during every code review, covering things commonly missed by standard review tools. This skill is primarily for reviewing Ruby code; some checks are Ruby-specific.

## Ruby: Prefer Enumerable Methods Over Mutating in `each`

Building a collection by mutating a variable inside an `each` block is almost always a sign that a more expressive Enumerable method exists. Flag these patterns and suggest the appropriate alternative. Common cases:

| Pattern | Preferred alternative |
|---|---|
| `each` + `<<` to collect results | `map` |
| `each` + conditional `<<` | `filter_map` |
| `each` + `<<` when condition may skip all | `select` / `reject` + `map` |
| `each` + accumulator variable | `reduce` / `each_with_object` |
| `each` + `break` / early return | `find` / `any?` / `all?` / `none?` |

The test: if the block writes to something outside itself, there is likely a better method. Use judgment — deeply nested or multi-step transformations may be clearer as explicit loops.

## Ruby: Avoid Unnecessary Indirection

Indirection has a cost: a method call instead of a direct read, a public interface that exists only to serve private code, an extracted method that requires a context switch to understand. Flag these patterns:

**Use ivars directly inside the class.** If a class accesses its own data through an `attr` reader internally, prefer the ivar directly (`@foo` instead of `foo`). Direct ivar access is faster and makes it immediately obvious at the call site that this is a local data read — not a computed property or something potentially expensive.

**Remove attrs used only internally.** If an `attr_reader` or `attr_accessor` is declared but never called from outside the class, the attr serves no purpose. Remove it and access the ivar directly throughout.

**Inline single-use methods.** If a method is short and has exactly one caller, consider inlining it. The extraction adds a navigation burden without adding reuse or clarity. This does not apply if the extracted name meaningfully communicates intent that would otherwise be lost.

## Ruby: Structure and Ordering

**Class layout.** Follow the standard Ruby class structure (https://rubystyle.guide/#consistent-classes): module inclusions, constants, macros (e.g. `attr_*`), class methods, then instance methods, with `private`/`protected` sections at the end. Flag deviations.

**Preserve existing ordering conventions.** If the surrounding code uses a consistent ordering — alphabetical methods, alphabetical `require` statements, alphabetical hash keys, sorted `case`/`when` branches, or any other explicit sequence — new entries must follow that same order. Flag insertions that break an existing sequence unless a comment explains why the ordering change is intentional.

## Ruby: Avoid `blank?` and `present?` Except on Strings

`blank?` and `present?` are ActiveSupport monkey-patches and should be treated as a last resort. Their only well-suited use is on `String`, where they detect whitespace-only values. On everything else, they are both slow and imprecise.

**Why they're slow:** On non-String objects, `blank?` dynamically checks whether `empty?` is defined, calls it if so, and returns `false` otherwise — with special cases hardcoded for `nil` and `false`. This dispatch cannot be cached and runs every call.

**Why they're imprecise:** They conflate distinct concepts. Use the check that matches the actual intent:

| Instead of | Use | When you mean |
|---|---|---|
| `foo.blank?` | `foo.nil?` | checking for nil |
| `foo.blank?` | `!foo` | checking for nil or false |
| `foo.blank?` | `foo.empty?` | checking an Array, Hash, or String is empty |
| `foo.present?` | `!foo.nil?` | checking non-nil |
| `foo.present?` | `foo` (in a conditional) | checking truthy |
| `foo.present?` | `!foo.empty?` | checking non-empty collection |

When reviewing, check Sorbet type signatures or use LSP to determine the type of the receiver and suggest the appropriate lightweight alternative. If the type is `String` and whitespace-only detection is plausible, `blank?` may be acceptable.

## Reserve "Request Changes" for Serious Issues

Only request changes when code is fundamentally broken or has a meaningful security vulnerability. For everything else — style preferences, minor improvements, alternative approaches — leave a comment instead. Defaulting to "request changes" for ordinary feedback is unnecessarily blocking and signals more severity than intended.

## Honesty Over Padding

If there are no issues, say so directly — "This looks great, no issues found." is a complete and valid review. Do not invent minor suggestions, nitpick style that doesn't matter, or add filler praise to justify the review. A clean bill of health is useful signal; padding obscures it.
