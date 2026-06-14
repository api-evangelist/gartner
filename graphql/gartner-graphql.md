# Gartner GraphQL Schema

Gartner is a global research and advisory firm delivering information, advice, and tools to business leaders across IT, finance, HR, legal, marketing, supply chain, and customer service functions. This conceptual GraphQL schema models the core domains of Gartner's platform: research documents, analyst profiles, vendor and product coverage, peer reviews, industry taxonomy, and enterprise access controls.

## Schema Overview

The schema is organized into the following domains:

### Research & Documents
Core research artifacts produced by Gartner analysts, including Hype Cycle reports, Magic Quadrant evaluations, Market Guides, Forecasts, Tech Profiles, Peer Insights, CIO Surveys, and IT Spend analysis. Each research item links to its underlying document, associated analysts, topics, and industries.

- `Research` — top-level research item with metadata, content type, and audience
- `ResearchDocument` — downloadable artifact with format, page count, and links
- `ResearchType` — enum covering HYPE_CYCLE, MAGIC_QUADRANT, MARKET_GUIDE, FORECAST, SURVEY, TECH_PROFILE, PEER_INSIGHTS, COMPETITIVE_LANDSCAPE, NOTE, and more
- `Note` — short-form analyst commentary linked to a topic
- `HypeReport` — Hype Cycle report for an emerging technology area
- `MagicQuadrant` — annual vendor positioning report by market
- `MarketGuide` — overview of a nascent or evolving market and its vendors
- `Forecast` — quantitative market forecast with growth projections
- `MarketForecast` — market-level forecast with total addressable market and regional breakdown
- `CompetitiveLandscape` — vendor competitive analysis for a given market
- `TechProfile` — maturity and adoption profile for a specific technology
- `PeerInsights` — aggregated peer reviews for a product
- `CIOSurvey` — annual CIO priorities survey with respondent data and top priorities
- `ITSpend` — IT spending data by segment, region, and year
- `TopPriority` — ranked priority item surfaced from CIO survey data

### Analysts
Gartner research is authored and delivered by named analysts with defined areas of expertise. Each analyst profile includes biographical details, topic and industry coverage, contact availability for client inquiries, and links to their published research.

- `Analyst` — named analyst with bio, expertise, contact info, and linked research
- `AnalystBio` — background, title, experience, education, and prior roles
- `AnalystExpertise` — specific area of expertise tied to technologies and industries
- `AnalystContact` — email, phone, social handles, and inquiry availability flag

### Topics & Taxonomy
Gartner organizes its content around a hierarchical taxonomy of topics, topic areas, and tags. Keywords support full-text discovery across the research corpus.

- `Topic` — named research topic linked to analysts, research, and topic area
- `TopicDetails` — description, related topics, and trending score
- `TopicArea` — grouping of related topics (e.g., Infrastructure, Security, AI)
- `TopicTag` — label/slug tag associated with a topic
- `Keyword` — term extracted from research content with frequency and related topics

### Industries & Sectors
Industry classification using standard coding schemes. Vendors and research are associated with one or more industries.

- `Industry` — named industry linked to research and vendors
- `IndustryCode` — standardized code (e.g., SIC, NAICS) for the industry
- `SectorCode` — sector and sub-sector classification

### Technology
Technologies are modeled as first-class entities with a type classification, maturity stage, and links to vendors, products, topics, and Hype Cycle reports.

- `Technology` — named technology with type enum, maturity stage, and vendor/product links
- `TechType` — enum: PLATFORM, APPLICATION, INFRASTRUCTURE, SECURITY, DATA_ANALYTICS, AI_ML, CLOUD, NETWORKING, DEVOPS, INTEGRATION, OTHER

### Products & Vendors
Vendors and their products are central to Gartner's evaluation work. Vendor profiles capture firmographic details and Magic Quadrant positioning. Products are linked to capability scores and peer reviews.

- `Vendor` — company with profile, products, industries, technologies, and services
- `VendorProfile` — firmographic data: HQ, revenue, employees, ticker, MQ position
- `VendorProduct` — versioned vendor-product association with certifications
- `Product` — individual product with category, capability scores, and peer insights
- `ProductCategory` — grouping of related products
- `CapabilityScore` — scored evaluation dimension for a product

### Reviews & Ratings
Peer reviews sourced from verified enterprise buyers, with detailed qualitative and quantitative feedback captured across multiple rating dimensions.

- `Review` — top-level review linked to a product and buyer
- `PeerReview` — peer review within the Peer Insights program
- `ReviewDetails` — pros, cons, summary, use case, implementation duration, and reviewer role
- `ReviewMetrics` — numeric scores for satisfaction, ease, features, support, and value
- `Rating` — aggregate rating with overall score and dimension breakdown
- `RatingDimension` — named scoring dimension with weight

### Buyers
Enterprise buyers are modeled with persona and company-size classification. Buyer feedback captures qualitative input outside of formal reviews.

- `Buyer` — buyer with persona enum, type, industry, and company size
- `BuyerPersona` — enum: CIO, CTO, CISO, VP_IT, IT_DIRECTOR, IT_MANAGER, BUSINESS_ANALYST, PROCUREMENT, OTHER
- `BuyerType` — enum: ENTERPRISE, MID_MARKET, SMB, GOVERNMENT, NONPROFIT, EDUCATION
- `BuyerFeedback` — free-form feedback tied to a product and buyer

### Content Classification
Content types, audiences, and tags allow research to be filtered and surfaced by the right role at the right stage of the buying cycle.

- `ContentType` — named content type associated with one or more ResearchType values
- `Audience` — named audience with persona list and role descriptions
- `ContentTag` — label/slug/category tag applied to research items

### Service Providers
Technology service providers and consulting firms that appear in Gartner coverage, including managed services and consulting practice areas.

- `ServiceProvider` — named service provider linked to a vendor
- `ManagedService` — managed service offering with technology and industry coverage
- `Consulting` — consulting practice with area, technologies, and industries

### Access & Licensing
Gartner content is gated by subscription. Enterprise licenses grant seat-based access and analyst inquiry hours. API access is managed through keys and bearer tokens.

- `ContentAccess` — access level, subscription requirement, and license/key links
- `EnterpriseLicense` — org-level license with tier, seats, expiry, and feature flags
- `APIKey` — API key with scopes, rate limit, and linked token
- `Token` — bearer token with type, scopes, and expiry

## Types Summary

| Domain | Types |
|---|---|
| Research & Documents | Research, ResearchDocument, ResearchType, Note, HypeReport, MagicQuadrant, PeerInsights, TechProfile, MarketGuide, Forecast, MarketForecast, CompetitiveLandscape, CIOSurvey, ITSpend, TopPriority |
| Analysts | Analyst, AnalystBio, AnalystExpertise, AnalystContact |
| Topics & Taxonomy | Topic, TopicDetails, TopicArea, TopicTag, Keyword |
| Industries & Sectors | Industry, IndustryCode, SectorCode |
| Technology | Technology, TechType |
| Products & Vendors | Vendor, VendorProfile, VendorProduct, Product, ProductCategory, CapabilityScore |
| Reviews & Ratings | Review, PeerReview, ReviewDetails, ReviewMetrics, Rating, RatingDimension |
| Buyers | Buyer, BuyerPersona, BuyerType, BuyerFeedback |
| Content Classification | ContentType, Audience, ContentTag |
| Service Providers | ServiceProvider, ManagedService, Consulting |
| Access & Licensing | ContentAccess, EnterpriseLicense, APIKey, Token |

Total named types: 55+

## Schema Source

`gartner-schema.graphql` — conceptual schema derived from Gartner's public documentation, product areas, and known platform capabilities. Gartner does not publish a public GraphQL API; this schema represents the logical data model inferred from their research, advisory, and peer review platform.
