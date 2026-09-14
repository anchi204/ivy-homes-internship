# Ivy Homes — Property Explorer

A full-stack property exploration web application built for the Ivy Homes Software Engineering Internship Assignment.

## Features

- Demo user authentication
- Secure server-side API key handling
- Access-token based sessions with automatic token refresh
- Property listings with pagination
- Search and property filters
- Property detail pages
- Save and unsave listings
- Saved listings page
- Rental properties
- Project listings with filters
- Insights dashboard
- Loading, empty and error states
- Responsive UI
- API investigation and documented inconsistencies

## Tech Stack

- Next.js
- React
- TypeScript
- Tailwind CSS
- Ivy Homes Property API
- Vercel

## Getting Started

Clone the repository and install dependencies:

    git clone https://github.com/anchi204/ivy-homes-internship.git
    cd ivy-homes-internship
    npm install

Create a `.env.local` file in the project root:

    IVY_API_KEY=your_api_key

The API base URL defaults to `https://solve.ivy.homes`.

Start the development server:

    npm run dev

Then open `http://localhost:3000`.

For a production build:

    npm run build

## Demo Login

Use any of the demo accounts provided in the assignment.

    Email: demo1@ivy.homes
    Password: 9beaaf0375

Other demo accounts:

    demo2@ivy.homes
    demo3@ivy.homes

## Project Structure

    app/
      api/
        auth/
        saved/
        session/
      insights/
      listings/
      login/
      projects/
      rentals/
      saved/

    components/
      ListingCard
      ListingFilterBar
      LoginForm
      LogoutButton
      NavLinks
      PaginationControls
      ProjectCard
      ProjectFilterBar
      RentalCard
      RentalFilterBar
      SaveButton
      SessionKeepAlive
      StatCard
      Header

    lib/
      ivy/
        auth.ts
        client.ts
        config.ts
        format.ts
        insights.ts
        listings.ts
        projects.ts
        rentals.ts
        saved.ts
        types.ts
      session.ts

    analysis/
      INVESTIGATION_LOG.md
      scripts/

## API Investigation

The provided API documentation was treated as a reference rather than the source of truth. The live API was tested directly to verify actual request parameters, responses and available endpoints.

### Important discrepancies found

- API authentication requires the `X-API-Key` header.
- Login returns `access_token`, `refresh_token`, `expires_in` and `refresh_url`; the documented `token` field was not present.
- The access token expires after approximately 15 minutes, so token refresh handling was implemented.
- The documented `page` parameter was ignored by the live API. Pagination works using `offset` and `limit`.
- The effective maximum `limit` was lower than the documented value.
- Collection responses use fields such as `limit`, `offset`, `count`, `total` and `has_more`.
- The listings endpoint can return inactive listings with `is_live: false`.
- The working listing detail route is `/v1/listings/{id}` rather than the documented singular route.
- The documented `/similar` endpoint was unavailable during testing.
- The documented analytics summary endpoint was unavailable, so the insights dashboard computes statistics from the available datasets.
- The documented favourites endpoint was unavailable. The working saved-listings endpoint is `/v1/saved`, using `listing_id`.
- Some project prices require Lakh/Crore conversion.
- Some project area values require unit normalization.

## Assignment Analysis

For the assigned New Gurgaon locality, the analysis produced:

| Metric | Result |
| --- | ---: |
| Total listing records | 3500 |
| Unique properties | 3254 |
| Active listings | 2792 |
| Total monthly rent | ₹49,22,000 |
| Average price/sqft for 2 BHK | ₹14,425.01 |
| Costliest project | P60060 |
| Costliest project maximum price | ₹5.83 Crore |
| Listings created in last 7 days | 129 |
| Projects with incorrect listing count | 295 |

Additional data-quality findings:

- 24 corrupt listing IDs were identified.
- 95 suspected fake listing IDs were identified.
- API-reported totals differed from the number of records retrievable through pagination.
- Project prices required normalization because of Lakh/Crore representations.
- Some project area values required unit conversion.

Detailed investigation notes are available in `analysis/INVESTIGATION_LOG.md`.

## Data Quality Handling

The application was implemented according to the behaviour observed from the live API.

This includes:

- Handling inactive listings
- Supporting offset-based pagination
- Normalizing project prices
- Handling different area units
- Handling missing or malformed listing data
- Showing appropriate empty and error states
- Computing insights locally when the analytics endpoint was unavailable

## What Turned Out Fine

The core functionality required for the assignment was available and usable after testing the live API:

- Demo authentication worked.
- Listings could be retrieved and paginated.
- Individual listings could be fetched.
- Saved-listing functionality was available through `/v1/saved`.
- Rental and project datasets were available.
- The required assignment analysis could be reproduced from the available API data.

The major challenges were inconsistencies between the written API documentation and the actual live API behaviour.

## Security

The Ivy Homes API key is stored only as a server-side environment variable and is never exposed to the browser.

The environment variable used is:

    IVY_API_KEY=...

Environment files are excluded from Git through `.gitignore`.

## Deployment

The application is deployed using Vercel.

For deployment, configure the following environment variable in the Vercel project:

    IVY_API_KEY

The API base URL does not need to be configured because the application defaults to:

    https://solve.ivy.homes

## Git Commit History

The project was developed incrementally with feature-based commits covering:

1. Initial project setup
2. Authentication and session handling
3. Property listings and filters
4. Listing detail page
5. Saved listings
6. Rentals and projects
7. Insights dashboard
8. API inconsistencies and pagination handling
9. Assignment analysis and answers
10. Documentation and submission files

The commit history reflects the progression of the implementation rather than a single final upload.

## AI Usage

AI assistance was used during development for implementation support, debugging, API reasoning, code review and documentation.

Important API behaviours were independently tested against the live API instead of relying only on the provided documentation.

## What I Would Improve With Two More Days

With additional development time, I would focus on:

- Improving overall UI/UX and visual polish
- Adding more comprehensive automated tests
- Improving client and server-side error handling
- Adding richer filtering and sorting
- Improving insights visualizations
- Adding property comparison functionality
- Better presentation of data-quality anomalies
- Improving accessibility
- Optimizing API requests and caching
- Adding stronger validation for edge cases

## Repository

GitHub: https://github.com/anchi204/ivy-homes-internship
## Demo

Live Demo: https://ivy-homes-internship-five.vercel.app/listings

Demo Login:
- Email: `demo1@ivy.homes`
- Password: `9beaaf0375`

Built for the Ivy Homes Software Engineering Internship Assignment — September 2026.
