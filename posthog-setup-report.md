<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the FashionHero Next.js App Router project. Here is a summary of all changes made:

- **`instrumentation-client.ts`** (new) — Initializes PostHog on the client side using the Next.js 15.3+ instrumentation pattern. Configured with a reverse proxy (`/ingest`), EU host, error tracking (`capture_exceptions`), and debug mode in development.
- **`next.config.ts`** — Added PostHog reverse-proxy rewrites (`/ingest/static/*`, `/ingest/array/*`, `/ingest/*` → EU PostHog endpoints) and `skipTrailingSlashRedirect: true`.
- **`.env.local`** — Added `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables.

Event tracking was added to 8 files covering the full user journey from product discovery to checkout.

| Event | Description | File |
|-------|-------------|------|
| `product_viewed` | User views a product detail page — top of conversion funnel | `src/app/products/[slug]/recently-viewed-section.tsx` |
| `add_to_cart` | User adds a product to the cart with color and size | `src/components/product-info.tsx` |
| `cart_item_removed` | User removes an item from the cart drawer | `src/components/cart-drawer.tsx` |
| `checkout_started` | User clicks CHECKOUT in the cart drawer | `src/components/cart-drawer.tsx` |
| `place_order_clicked` | User clicks PLACE ORDER on checkout page | `src/app/checkout/page.tsx` |
| `paragon_for_husband_configured` | User configures the Paragon for Husband discount | `src/app/checkout/page.tsx` |
| `quick_view_opened` | User opens the quick view modal for a product | `src/components/product-card.tsx` |
| `search_performed` | User performs a product search (on Enter key) | `src/components/search-modal.tsx` |
| `search_result_clicked` | User clicks a product from search results | `src/components/search-modal.tsx` |
| `wishlist_toggled` | User adds or removes a product from the wishlist | `src/components/wishlist-button.tsx` |
| `user_signed_in` | User signs in — triggers `posthog.identify()` | `src/app/account/login/page.tsx` |
| `user_registered` | User registers — triggers `posthog.identify()` | `src/app/account/register/page.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- [Analytics basics dashboard](/dashboard/675498)
- [Purchase Conversion Funnel](/insights/1KudlbDc) — Full 4-step conversion funnel: product viewed → add to cart → checkout started → place order clicked
- [Add to Cart Volume](/insights/0GrT31tU) — Daily trend of add to cart events
- [New User Registrations](/insights/srKfNXuQ) — Registrations and sign-ins over time
- [Search Engagement](/insights/ycEPQCIo) — Searches performed vs. results clicked over time
- [Wishlist Activity](/insights/yOB59S3a) — Wishlist toggle events over time

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
