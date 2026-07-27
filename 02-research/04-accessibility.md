# Accessibility requirements

Hold should aim for WCAG 2.2 AA where applicable and test beyond compliance with users who have cognitive, learning, visual, motor and fatigue-related access needs.

## Minimum requirements

- Normal text contrast of at least 4.5:1
- Large text contrast of at least 3:1
- Meaningful controls and states at least 3:1
- Never communicate status by colour alone
- Support dynamic text and zoom
- Use real text, not images of text
- Maintain visible focus states
- Provide sufficiently large touch targets
- Respect reduced-motion settings
- Support screen readers
- Avoid drag-only interactions
- Avoid short timeouts
- Test for dyslexia and cognitive accessibility

## Hold-specific requirements

- Primary action prominent but not aggressive
- Back and cancel in consistent locations
- No low-contrast grey-on-cream
- Important meaning not hidden inside icons
- Sentence case
- Left-aligned body text
- Short paragraphs
- Destructive actions separated from primary actions
- Recipient selection reversible and visible
- Native autocorrect, spellcheck and predictive text always enabled on every message input, exactly like composing a normal text — never a custom or stripped-down keyboard. This is an accessibility requirement, not just parity: cognitive fog, fatigue, ADHD and medication effects are common among Hold's users, and native input assistance lowers composition effort

## Sources

- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- WCAG 2.2 Quick Reference: https://www.w3.org/WAI/WCAG22/quickref/
- Icon comprehension under cognitive/literacy load — abstract icons are frequently misread without an accompanying label; text+icon combinations reduce cognitive effort versus icon-only or text-only, and recognition (seeing a labelled icon) requires less cognitive processing than recall (interpreting an unlabelled one). This directly informs the "important meaning not hidden inside icons" requirement above and the labelled bottom-navigation icons in `04-ux-content/04-navigation-architecture.md`.
