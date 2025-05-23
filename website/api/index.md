# API Reference

The ally-bcp-47 library provides a comprehensive set of functions for working with BCP-47 language tags.

## Core Functions

### validateLanguageTag(tag, options?)

The primary function for validating language tags. Returns a detailed validation result.

```typescript
import { validateLanguageTag } from "@aleksejdix/ally-bcp47";

const result = validateLanguageTag("en-US");
console.log(result.isValid); // true
console.log(result.isWellFormed); // true
console.log(result.tag); // { tag: 'en-US', language: 'en', region: 'us' }
```

[Learn more about validateLanguageTag](/api/validate-language-tag)

### isValid(tag)

A convenience function that returns true if a tag is valid (well-formed and all subtags exist in the registry).

```typescript
import { isValid } from "@aleksejdix/ally-bcp47";

console.log(isValid("en-US")); // true
console.log(isValid("en-ZZ")); // false (ZZ is not a valid region code)
```

[Learn more about isValid](/api/is-valid)

### isWellFormed(tag)

A convenience function that returns true if a tag is well-formed according to BCP-47 syntax rules.

```typescript
import { isWellFormed } from "@aleksejdix/ally-bcp47";

console.log(isWellFormed("en-US")); // true
console.log(isWellFormed("en--US")); // false (double hyphen is not allowed)
```

[Learn more about isWellFormed](/api/is-well-formed)

### parseTag(tag)

Parses a language tag into its component parts.

```typescript
import { parseTag } from "@aleksejdix/ally-bcp47";

const parsed = parseTag("en-US");
console.log(parsed); // { language: 'en', region: 'us' }
```

[Learn more about parseTag](/api/parse-tag)

### canonicalizeTag(tag)

Canonicalizes a language tag to its preferred form.

```typescript
import { canonicalizeTag } from "@aleksejdix/ally-bcp47";

console.log(canonicalizeTag("en-us")); // 'en-US'
console.log(canonicalizeTag("zh-hans-cn")); // 'zh-CN'
```

[Learn more about canonicalizeTag](/api/canonicalize-tag)

### isValidLanguageTag(tag)

A simplified validation function using regular expressions.

```typescript
import { isValidLanguageTag } from "@aleksejdix/ally-bcp47";

console.log(isValidLanguageTag("en-US")); // true
console.log(isValidLanguageTag("123")); // false (language must start with a letter)
```

[Learn more about isValidLanguageTag](/api/is-valid-language-tag)

### getLanguageDisplayName(tag, displayLocale?)

Converts a language tag to a human-readable language name.

```typescript
import { getLanguageDisplayName } from "@aleksejdix/ally-bcp47";

console.log(getLanguageDisplayName("en")); // "English"
console.log(getLanguageDisplayName("fr", "de")); // "Französisch"
```

[Learn more about getLanguageDisplayName](/api/get-language-display-name)

## Types

The library exports TypeScript types for all objects and functions:

```typescript
import {
  ValidationResult,
  ValidationError,
  ValidationWarning,
  LanguageTag,
} from "@aleksejdix/ally-bcp47";
```

## Error Handling

All validation functions provide detailed error information:

```typescript
const result = validateLanguageTag("en-UK");

if (!result.isValid && result.errors) {
  for (const error of result.errors) {
    console.log(`Error: ${error.message}`);
    if (error.suggestedReplacement) {
      console.log(`Suggested fix: ${error.suggestedReplacement}`);
    }
  }
}
```

## Registry Functions

The library also provides low-level functions for working directly with the registry:

```typescript
import {
  isValidLanguageCode,
  isValidScriptCode,
  isValidRegionCode,
} from "@aleksejdix/ally-bcp47";

console.log(isValidLanguageCode("en")); // true
console.log(isValidScriptCode("Latn")); // true
console.log(isValidRegionCode("US")); // true
```
