# Supplemental Code Review Checks

These are additional checks to apply during every code review, covering things commonly missed by standard review tools.

## Reserve "Request Changes" for Serious Issues

Only request changes when code is fundamentally broken or has a meaningful security vulnerability. For everything else — style preferences, minor improvements, alternative approaches — leave a comment instead. Defaulting to "request changes" for ordinary feedback is unnecessarily blocking and signals more severity than intended.

## Honesty Over Padding

If there are no issues, say so directly — "This looks great, no issues found." is a complete and valid review. Do not invent minor suggestions, nitpick style that doesn't matter, or add filler praise to justify the review. A clean bill of health is useful signal; padding obscures it.
