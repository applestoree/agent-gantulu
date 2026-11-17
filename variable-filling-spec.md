# Variable Filling Specification

**Version:** 1.0  
**Status:** Approved  
**Project:** agent-gantulu

## 1. Purpose

This document defines how variables in `template-prompt.md` are populated to produce a complete AI image-generation prompt.

## 2. Architecture Decision

- `template-prompt.md` remains a static prompt template.
- The Prompt Builder is responsible for resolving and replacing every template variable.
- Product data is sourced from `products.json`.
- AI-generated content and visual decisions are supplied to the Prompt Builder as variable values.
- The Prompt Builder combines the resolved values with the static template; it does not change the template's structure.

## 3. Variable Mapping

| Template variable | Source | Population rule |
|---|---|---|
| `{{products}}` | `products.json` | Map the selected product record's `product` field to the template variable. |
| `{{headline}}` | AI Content Generator | Generate a headline based on the selected product and the content objective. |
| `{{subheadline}}` | AI Content Generator | Generate supporting copy consistent with the headline and product. |
| `{{features}}` | `products.json` | Use the selected product record's `features` array. Format its items as readable prompt text. |
| `{{composition}}` | AI Visual Director | Determine the product and supporting-element arrangement. |
| `{{layout}}` | Layout Configuration / AI Visual Director | Select a layout from the available layout definitions. |
| `{{background}}` | Background Configuration / AI Visual Director | Select a permitted background preset. |
| `{{quality}}` | System Configuration | Use the configured visual-quality instruction. |

## 4. Data Source Rules

1. Product records must be retrieved from `products.json`.
2. The selected product ID identifies the product record.
3. The template variable `{{products}}` receives the value of the record's `product` field. The source field name and template variable name are intentionally different.
4. The `{{features}}` variable receives only features belonging to the selected product record.
5. AI must not invent, alter, or add product specifications or features.
6. If the selected product ID does not exist, prompt generation must stop and report that the product was not found.

## 5. AI Generation Responsibilities

### AI Content Generator
- Produces `headline` and `subheadline`.
- Uses the selected product data as factual context.
- Must not introduce unsupported product claims.

### AI Visual Director
- Determines `composition`.
- Selects an available `layout`.
- Selects an available `background` preset.
- Must follow the available configuration definitions and the product's visual context.

### System Configuration
- Supplies the `quality` value.
- Keeps quality instructions consistent unless an authorized configuration changes them.

## 6. Prompt Builder Responsibilities

The Prompt Builder must:

1. Load the static `template-prompt.md`.
2. Receive the selected product ID and resolve its record from `products.json`.
3. Obtain the generated content and visual-configuration values.
4. Map source values to the exact template variable names.
5. Format array values such as `features` into readable text.
6. Replace every supported placeholder in the template.
7. Validate that no unresolved placeholder remains.
8. Return the completed prompt without modifying or rewriting the source template.

## 7. Validation and Error Handling

- Required variables must have non-empty values before prompt completion.
- Missing product records, missing required values, or unresolved placeholders must produce an explicit error.
- The Prompt Builder must not silently invent fallback product data or unsupported visual settings.
- A failed validation must prevent the incomplete prompt from being presented as final.

## 8. Illustrative Variable Object

The following is an example of the resolved data structure passed to the Prompt Builder. AI-generated values are illustrative.

```json
{
  "products": "Apple iPhone 17 Pro",
  "headline": "POWER. PRO. UNLEASHED.",
  "subheadline": "Experience the next level of performance.",
  "features": [
    "A19 Pro chip",
    "Pro Fusion 48MP camera system",
    "Super Retina XDR display",
    "Aluminum unibody design"
  ],
  "composition": "Hero product centered with three-quarter angle",
  "layout": "Premium Product Hero",
  "background": "Clean White Premium",
  "quality": "High-resolution commercial photography, realistic details, professional studio lighting"
}
```

## 9. Scope Boundary

This specification defines variable sources, mapping, responsibilities, and validation for Prompt Builder V1.0.

It does not authorize changes to the contents or structure of `template-prompt.md`, changes to `products.json` schema, or implementation of additional features beyond this specification.
