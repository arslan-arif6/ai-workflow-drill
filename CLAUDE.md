# Project Rules

1. Never treat HTML5 attributes (like `required`) as a substitute for real 
   validation logic — always implement explicit format checks in JavaScript 
   when "validation" is requested, not just native browser behavior.

2. Every form field with validation must have a visible inline error message 
   tied to a specific element (e.g. `#fieldError`), not just a browser 
   tooltip — errors should be testable and stylable.

3. Before returning validation code, self-test it against edge cases (empty 
   input, malformed input, valid input) and report the results — don't 
   assume correctness without verification.
   