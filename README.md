Experiment: Samsung UK Cart — Console-ready JavaScript
Below is a single pasteable JavaScript snippet you can run from the browser console on https://www.samsung.com/uk/cart (or the cart page after adding a Galaxy Z Fold7). It implements the four required changes:
• 	Voucher Input UX Variant — replaces the always-visible voucher input with a “Have a voucher?” toggle link that reveals the original voucher input and preserves its behavior.
• 	Holiday Returns Badge — reuses the existing holiday returns banner node and moves it into a compact badge near the order total / checkout area; hides the original banner.
• 	Inline Trade-In Value Teaser — injects a small, focusable teaser under each product price that opens the existing Trade-In flow when clicked; hides the original Trade-In card visually but keeps functionality.
• 	Brand-aware Dynamic Trade-In Copy — adjusts the trade-in copy to mention the detected brand and, when possible, shows the maximum discount value extracted from the page’s trade-in data.
The script is defensive: it waits for elements to appear, avoids duplicates, uses  to survive re-renders, injects CSS dynamically, and does not remove original functionality.

How to run
1. 	Open the Samsung UK cart page () after adding a Galaxy Z Fold7.
2. 	Open DevTools → Console.
3. 	Paste the entire code block below and press Enter.
4. 	Call the entry function if needed (the script auto-initialises). The entry function is .



Notes, assumptions & limitations
• 	Selectors & heuristics: Samsung’s live site may use different class names or markup. The script uses robust heuristics (text matching, multiple selector fallbacks) to find voucher forms, summary panels, trade-in sections and cart items. In rare cases where the page structure is very different, the script may not find the target nodes — it fails gracefully (no errors) and logs a warning to the console.
• 	Reusing DOM nodes: The holiday badge reuses the banner text and hides the original banner () so scripts that rely on it continue to work. The trade-in section is visually hidden via an accessible technique () so the underlying functionality remains.
• 	Trade-in amounts: The script attempts to extract trade-in values from the page (DOM text, inline JSON in scripts, or a few window properties). This is intentionally conservative and local-only (no external API calls). If no amounts are found, the teaser falls back to brand-aware copy without an amount.
• 	Brand detection: Uses  and  heuristics. If brand cannot be determined, it falls back to “Any Smartphone” or “your smartphone”.
• 	No duplication: Each injected element uses data attributes and checks to avoid duplicates on re-renders.
• 	Accessibility: Teasers are focusable and keyboard-activatable. The original trade-in UI remains in the DOM so screen readers and scripts can still access it.
• 	Performance: Uses a  with a small debounce to re-run idempotent initialization when the cart re-renders. Waiting timeouts are conservative to avoid long polling.
• 	Visual styling: CSS is injected dynamically and kept lightweight to match Samsung’s visual language (neutral background, Samsung-blue link color). You can tweak the CSS in the  function.
