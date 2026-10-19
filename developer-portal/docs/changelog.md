# Changelog

## [1.0.0] - 2026-10-19

### Added

**Endpoints**

- `POST /plans` *(Plans)* — Create plan
- `GET /plans/{id}` *(Plans)* — Get plan by ID
- `PATCH /plans/{id}` *(Plans)* — Update plan
- `POST /payments` *(Payments)* — Record or initiate payment

**Schemas**

- Added schema `AnalyticsQuery`
- Added schema `ApiKeyInput`
- Added schema `CorsPolicy`
- Added schema `FallbackChain`
- Added schema `ForecastRequest`
- Added schema `Meta`
- Added schema `PaymentInput`
- Added schema `PlanInput`
- Added schema `PlanUpdate`
- Added schema `RefundInput`
- Added schema `StandardErrorEnvelope`
- Added schema `SubscriptionCancel`
- Added schema `SubscriptionPause`
- Added schema `SubscriptionUpdate`

### Changed

**Endpoints**

- `GET /subscriptions` — List subscriptions
  - Added parameter `customerId` (query) *(optional)*
  - Added parameter `planId` (query) *(optional)*
  - Added parameter `cursor` (query) *(optional)*
  - **[Breaking]** Removed parameter `category` (query)
  - Added response `401`
- `POST /subscriptions` — Create subscription
  - Added response `422`
- `PUT /subscriptions/{id}` — Update subscription
  - Added response `404`
  - Added response `422`
- `DELETE /subscriptions/{id}` — Delete subscription
  - Added response `404`
- `POST /subscriptions/{id}/cancel` — Cancel subscription
  - Request body: **[Breaking]** Removed field `atPeriodEnd`
  - Request body: **[Breaking]** Removed field `reason`
  - Added response `404`
- `GET /plans` — List plans
  - Added parameter `active` (query) *(optional)*
  - Added parameter `currency` (query) *(optional)*
  - Added parameter `cursor` (query) *(optional)*
  - Added parameter `limit` (query) *(optional)*
  - Added parameter `page` (query) *(optional)*
  - Response `200` schema changed:
    - Added field `meta` *(required)*
    - Added field `pagination` *(optional)*
    - **[Breaking]** Field `data` is now required
    - **[Breaking]** Field `success` is now required
  - Security requirements changed
- `GET /payments` — List payments
  - Added parameter `customerId` (query) *(optional)*
  - Added parameter `status` (query) *(optional)*
  - Added parameter `cursor` (query) *(optional)*
  - Added parameter `limit` (query) *(optional)*
  - Added response `401`
  - Response `200` schema changed:
    - **[Breaking]** Removed field `data`
    - **[Breaking]** Removed field `pagination`
    - **[Breaking]** Removed field `success`
- `GET /invoices` — List invoices
  - Added parameter `subscriptionId` (query) *(optional)*
  - Added parameter `status` (query) *(optional)*
  - Added response `401`
  - Response `200` schema changed:
    - **[Breaking]** Removed field `data`
    - **[Breaking]** Removed field `success`
- `GET /webhooks` — List webhooks
  - Added response `401`
  - Response `200` schema changed:
    - **[Breaking]** Removed field `data`
    - **[Breaking]** Removed field `success`
- `POST /webhooks` — Create webhook endpoint
  - Added response `422`
  - Response `201` schema changed:
    - **[Breaking]** Removed field `data`
    - **[Breaking]** Removed field `success`
- `GET /analytics/usage` — Get usage analytics
  - Added parameter `startDate` (query) *(optional)*
  - Added parameter `endDate` (query) *(optional)*
  - Added parameter `granularity` (query) *(optional)*
  - Added response `401`
  - Response `200` schema changed:
    - Added field `activeSubscriptions` *(optional)*
    - Added field `period` *(optional)*
    - Added field `revenue` *(optional)*
    - Added field `totalRequests` *(optional)*
    - **[Breaking]** Removed field `data`
    - **[Breaking]** Removed field `success`
- `GET /themes` — Get theme settings
  - Response `200` schema changed:
    - **[Breaking]** Removed field `data`
    - **[Breaking]** Removed field `success`
  - Security requirements changed

**Schemas**

- Schema `Invoice` changed:
  - Added field `amount` *(optional)*
  - Added field `dueDate` *(optional)*
  - **[Breaking]** Removed field `dueAt`
  - **[Breaking]** Removed field `total`
- Schema `Pagination` changed:
  - Added field `hasMore` *(optional)*
  - Added field `nextCursor` *(optional)*
  - **[Breaking]** Removed field `hasNext`
  - **[Breaking]** Removed field `page`
  - **[Breaking]** Removed field `total`
- Schema `Payment` changed:
  - **[Breaking]** Removed field `subscriptionId`
- Schema `Plan` changed:
  - Added field `active` *(optional)*
  - Added field `amount` *(optional)*
  - Added field `description` *(optional)*
  - **[Breaking]** Removed field `price`
- Schema `Subscription` changed:
  - Added field `currentPeriodEnd` *(optional)*
  - Added field `currentPeriodStart` *(optional)*
  - Added field `planId` *(optional)*
  - Added field `userId` *(optional)*
  - **[Breaking]** Removed field `billingCycle`
  - **[Breaking]** Removed field `category`
  - **[Breaking]** Removed field `currency`
  - **[Breaking]** Removed field `name`
  - **[Breaking]** Removed field `nextBillingDate`
  - **[Breaking]** Removed field `price`
- Schema `SubscriptionInput` changed:
  - Added field `customerId` *(required)*
  - Added field `metadata` *(optional)*
  - Added field `paymentMethodId` *(required)*
  - Added field `planId` *(required)*
  - Added field `trialEnd` *(optional)*
  - **[Breaking]** Removed field `billingCycle`
  - **[Breaking]** Removed field `category`
  - **[Breaking]** Removed field `currency`
  - **[Breaking]** Removed field `name`
  - **[Breaking]** Removed field `price`
  - **[Breaking]** Removed field `startDate`
- Schema `SubscriptionList` changed:
  - **[Breaking]** Removed field `success`
- Schema `WebhookInput` changed:
  - Added field `active` *(required)*
  - Added field `metadata` *(optional)*
  - Added field `secret` *(optional)*

**Security**

- Security scheme `BearerAuth` updated

All notable changes to the SubTrackr API and SDKs will be documented in this file.

## [1.2.0] - 2026-07-24

### Added
- **API Playground**: Interactive API playground added to the developer portal for easy testing and code generation.
- **Python SDK**: Added support for pagination in the `list` method for subscriptions and payments.
- **Go SDK**: Added webhook verification helpers.

### Changed
- Improved error messages for `INVALID_REQUEST` by providing more granular `details`.

## [1.1.0] - 2026-06-15

### Added
- **Webhooks**: Added `invoice.generated` event.
- **API**: New `GET /v1/analytics/subscriptions` endpoint for aggregated subscription metrics.

### Fixed
- Fixed an issue where the `category` filter on `GET /v1/subscriptions` was case-sensitive.

## [1.0.0] - 2026-05-01

### Added
- Initial stable release of the SubTrackr API (`v1`).
- SDKs released for JavaScript/Node.js, Python, and Go.
- comprehensive Developer Portal with API Reference and Quick Start Guides.
