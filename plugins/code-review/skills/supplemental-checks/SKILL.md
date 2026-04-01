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

## Reserve "Request Changes" for Serious Issues

Only request changes when code is fundamentally broken or has a meaningful security vulnerability. For everything else — style preferences, minor improvements, alternative approaches — leave a comment instead. Defaulting to "request changes" for ordinary feedback is unnecessarily blocking and signals more severity than intended.

## Honesty Over Padding

If there are no issues, say so directly — "This looks great, no issues found." is a complete and valid review. Do not invent minor suggestions, nitpick style that doesn't matter, or add filler praise to justify the review. A clean bill of health is useful signal; padding obscures it.
