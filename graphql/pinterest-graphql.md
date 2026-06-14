# Pinterest GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Pinterest API v5. Pinterest is a visual discovery platform enabling users to save, organize, and discover ideas through images, videos, and links organized on boards. The REST API v5 covers pins, boards, users, advertising, catalogs, conversions, and analytics.

**Base REST API:** https://api.pinterest.com/v5  
**Developer Documentation:** https://developers.pinterest.com/docs/api/v5/  
**GitHub:** https://github.com/pinterest

---

## Schema Source

This GraphQL schema is derived from the Pinterest REST API v5 surface, translating resource endpoints and their data models into a unified GraphQL type system. Pinterest does not publish an official GraphQL API; this schema is a conceptual mapping intended for tooling, documentation, and integration planning.

---

## Core Domain Areas

### Pins

Pins are the fundamental unit of content on Pinterest. A pin represents a saved idea — an image, video, or link — that can be saved to a board.

- **Pin** — Core pin object with id, title, description, link, media, and board association
- **PinDetails** — Extended pin data including analytics and creative metadata
- **PinImage** — Image media attached to a pin (original, resized variants)
- **PinVideo** — Video media attached to a pin with cover image and duration
- **PinMedia** — Union of image and video pin media
- **PinCreative** — Creative assets for promoted or story pins
- **PinAd** — Promoted pin used in advertising campaigns
- **PinAnalytics** — Engagement metrics for a pin over a date range
- **PinMetrics** — Aggregated lifetime and daily metrics for a pin
- **StoryPin** — Multi-page story format pin with pages and blocks

### Boards

Boards are named collections of pins that belong to a user.

- **Board** — Core board object with id, name, description, owner, and privacy setting
- **BoardDetails** — Extended board data including follower counts and pin counts
- **BoardSection** — Named sub-section within a board for organizing pins
- **BoardSectionPin** — Pin membership in a board section
- **BoardCover** — Cover image configuration for a board
- **BoardFollowers** — Paginated list of users following a board

### Users and Accounts

- **User** — Authenticated Pinterest user account
- **UserProfile** — Public-facing profile fields (username, bio, website, follower counts)
- **UserAnalytics** — Account-level analytics including impressions and engagement
- **PublicUser** — Publicly visible user data without private fields
- **LinkedBusinessAccount** — Business account linked to a personal user account
- **BusinessAccount** — Pinterest business account for advertising and analytics
- **BusinessProfile** — Public profile of a business account

### Advertising

- **AdAccount** — Top-level advertising account container
- **AdAccountBudget** — Budget configuration and spend tracking for an ad account
- **Campaign** — Advertising campaign grouping ad groups under a shared objective
- **CampaignAnalytics** — Performance metrics for a campaign over a date range
- **AdGroup** — Group of ads within a campaign sharing targeting and budget
- **AdGroupAnalytics** — Performance metrics for an ad group
- **Ad** — Individual advertisement unit associated with a pin
- **AdCreative** — Creative specification for an ad (image, video, copy)
- **AdTargeting** — Targeting parameters for an ad group (demographics, interests, keywords)

### Audiences

- **Audience** — Defined audience segment for ad targeting
- **AudienceSource** — Data source definition for building an audience
- **AudienceInsights** — Demographic and behavioral insights about an audience segment
- **CustomerList** — Uploaded customer data (emails, MAIDs) for audience matching
- **Interest** — Pinterest interest category used for targeting
- **Keyword** — Keyword used in search-based ad targeting
- **KeywordMetrics** — Historical performance metrics for a keyword

### Conversions

- **Conversion** — Recorded conversion event attributed to a Pinterest ad
- **ConversionEvent** — Single conversion event payload sent via the Conversions API
- **ConversionTag** — JavaScript tag placed on an advertiser's site for conversion tracking
- **ConversionReport** — Aggregated conversion report for an ad account or campaign

### Catalogs

- **CatalogFeed** — Product feed file ingested by Pinterest for shopping ads
- **CatalogProduct** — Individual product item from a catalog feed
- **CatalogIngestion** — Status and results of a catalog feed ingestion run
- **ProductGroup** — Group of catalog products filtered by attributes for targeting
- **ProductGroupPromotion** — Promotion configuration linking a product group to an ad
- **ShoppingAd** — Ad type that dynamically pulls creative from a catalog product

### Platform and Auth

- **OAuthApp** — Registered OAuth application with client credentials
- **AccessToken** — OAuth 2.0 access token with scopes and expiry
- **Scope** — Individual OAuth permission scope
- **Webhook** — Registered webhook endpoint for Pinterest event notifications
- **Notification** — Notification event delivered to a registered webhook
- **APIKey** — API key credential for server-to-server access
- **RateLimit** — Rate limit configuration and current usage for an API category

---

## Query Operations

| Query | Description |
|---|---|
| `pin(id: ID!)` | Fetch a single pin by ID |
| `pins(boardId: ID!, first: Int, after: String)` | List pins on a board |
| `board(id: ID!)` | Fetch a single board by ID |
| `boards(userId: ID, first: Int, after: String)` | List boards for a user |
| `boardSections(boardId: ID!)` | List sections within a board |
| `user(username: String!)` | Fetch a public user profile |
| `me` | Fetch the authenticated user's account |
| `pinAnalytics(pinId: ID!, startDate: String!, endDate: String!)` | Get analytics for a pin |
| `userAnalytics(startDate: String!, endDate: String!)` | Get analytics for the authenticated user |
| `adAccount(id: ID!)` | Fetch an ad account |
| `adAccounts(first: Int, after: String)` | List ad accounts |
| `campaigns(adAccountId: ID!)` | List campaigns in an ad account |
| `campaign(adAccountId: ID!, campaignId: ID!)` | Fetch a single campaign |
| `adGroups(adAccountId: ID!, campaignId: ID!)` | List ad groups in a campaign |
| `ads(adAccountId: ID!, adGroupId: ID!)` | List ads in an ad group |
| `audiences(adAccountId: ID!)` | List audiences for an ad account |
| `keywords(adAccountId: ID!)` | List keywords for an ad account |
| `catalogFeeds(adAccountId: ID!)` | List catalog feeds |
| `catalogProducts(catalogId: ID!, first: Int, after: String)` | List products in a catalog |
| `productGroups(adAccountId: ID!)` | List product groups |
| `conversionTags(adAccountId: ID!)` | List conversion tags |
| `webhooks` | List registered webhooks |
| `rateLimit(category: String!)` | Get rate limit status for a category |

---

## Mutation Operations

| Mutation | Description |
|---|---|
| `createPin(input: CreatePinInput!)` | Create a new pin |
| `updatePin(id: ID!, input: UpdatePinInput!)` | Update an existing pin |
| `deletePin(id: ID!)` | Delete a pin |
| `createBoard(input: CreateBoardInput!)` | Create a new board |
| `updateBoard(id: ID!, input: UpdateBoardInput!)` | Update an existing board |
| `deleteBoard(id: ID!)` | Delete a board |
| `createBoardSection(boardId: ID!, input: CreateBoardSectionInput!)` | Create a board section |
| `updateBoardSection(boardId: ID!, sectionId: ID!, input: UpdateBoardSectionInput!)` | Update a board section |
| `deleteBoardSection(boardId: ID!, sectionId: ID!)` | Delete a board section |
| `createCampaign(adAccountId: ID!, input: CreateCampaignInput!)` | Create an ad campaign |
| `updateCampaign(adAccountId: ID!, campaignId: ID!, input: UpdateCampaignInput!)` | Update a campaign |
| `createAdGroup(adAccountId: ID!, input: CreateAdGroupInput!)` | Create an ad group |
| `createAd(adAccountId: ID!, input: CreateAdInput!)` | Create an ad |
| `updateAd(adAccountId: ID!, adId: ID!, input: UpdateAdInput!)` | Update an ad |
| `createAudience(adAccountId: ID!, input: CreateAudienceInput!)` | Create an audience segment |
| `createCustomerList(adAccountId: ID!, input: CreateCustomerListInput!)` | Create a customer list |
| `createCatalogFeed(adAccountId: ID!, input: CreateCatalogFeedInput!)` | Create a catalog feed |
| `createConversionTag(adAccountId: ID!, input: CreateConversionTagInput!)` | Create a conversion tag |
| `sendConversionEvents(adAccountId: ID!, events: [ConversionEventInput!]!)` | Send conversion events |
| `createWebhook(input: CreateWebhookInput!)` | Register a webhook |
| `deleteWebhook(id: ID!)` | Delete a webhook |

---

## Authentication

The Pinterest API uses OAuth 2.0. Applications must obtain an access token with the appropriate scopes before making API calls. Available scopes include `pins:read`, `pins:write`, `boards:read`, `boards:write`, `ads:read`, `ads:write`, `catalogs:read`, `catalogs:write`, `user_accounts:read`, and `user_accounts:write`.

---

## Rate Limits

API requests are rate-limited per category. Key limits on the Standard tier include:

- Org Read: 1,000 requests/minute
- Ads Read: 120,000 requests/minute
- Ads Write: 400 requests/minute
- Catalog Read/Write: 100 requests/minute
- Org Analytics: 60 requests/minute

---

## References

- Pinterest API v5 Documentation: https://developers.pinterest.com/docs/api/v5/
- Pinterest GitHub Organization: https://github.com/pinterest
- Pinterest API Description (OpenAPI): https://github.com/pinterest/api-description
- Pinterest Developer Portal: https://developers.pinterest.com/
- Pinterest Status: https://www.pintereststatus.com/
