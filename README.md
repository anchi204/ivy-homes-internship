# Ivy Homes — Property Explorer

A full-stack property browsing application built for the Ivy Homes Software Engineering Internship Assignment (September 2026).

The application integrates with the Ivy Homes Property API and provides property discovery, filtering, listing details, saved listings, rentals, projects, and an insights dashboard.

## Features

### Authentication
- Login using the real Ivy Homes authentication API
- Session persistence across page refreshes
- Access-token based authentication
- Automatic token refresh for longer sessions
- Logout functionality

### Property Listings
- Browse property listings
- Pagination using the API's offset-based pagination
- Filter listings by:
  - Locality
  - Bedrooms
  - Price range
  - Furnishing
- Listing cards with important property information
- Clear handling of unavailable or inactive listings

### Listing Details
- Dedicated detail page for every listing
- Property information including:
  - Price
  - Bedrooms
  - Area
  - Locality
  - Furnishing
  - Contact information
- Listings are accessible through individual URLs

### Saved Listings
- Save and unsave properties
- View all saved listings
- Saved listings are associated with the logged-in user
- Saved state persists across page reloads and re-login

### Rentals
- Browse rental properties
- Rental filtering
- Correct handling and display of rental prices
- Pagination

### Projects
- Browse property projects
- Project filtering
- Correct project price interpretation
- Correct handling of area units
- Project listing information

### Insights
- Dashboard containing useful property-market statistics
- Insights computed from the available API datasets
- Highlights data-quality and API inconsistencies discovered during investigation

## Tech Stack

- Next.js
- React
- TypeScript
- Tailwind CSS
- Ivy Homes Property API

## Project Structure

```text
ivy-homes-internship/
│
├── app/
│   ├── api/
│   │   ├── auth/
│   │   │   ├── login/
│   │   │   └── logout/
│   │   ├── saved/
│   │   └── session/
│   │
│   ├── insights/
│   ├── listings/
│   │   └── [id]/
│   ├── login/
│   ├── projects/
│   ├── rentals/
│   └── saved/
│
├── components/
│   ├── ListingCard
│   ├── ListingFilterBar
│   ├── LoginForm
│   ├── LogoutButton
│   ├── NavLinks
│   ├── PaginationControls
│   ├── ProjectCard
│   ├── ProjectFilterBar
│   ├── RentalCard
│   ├── RentalFilterBar
│   ├── SaveButton
│   ├── SessionKeepAlive
│   └── StatCard
│
├── lib/
│   ├── ivy/
│   │   ├── auth.ts
│   │   ├── client.ts
│   │   ├── config.ts
│   │   ├── format.ts
│   │   ├── insights.ts
│   │   ├── listings.ts
│   │   ├── projects.ts
│   │   ├── rentals.ts
│   │   ├── saved.ts
│   │   └── types.ts
│   │
│   ├── session.ts
│   └── session-shared.ts
│
├── analysis/
│   ├── INVESTIGATION_LOG.md
│   └── scripts/
│
├── README.md
├── submission.json
└── package.json
Prerequisites
Node.js
npm
1. Clone the repository
git clone https://github.com/anchi204/ivy-homes-internship.git
cd ivy-homes-internship
2. Install dependencies
npm install
3. Configure environment variables

Create a .env.local file in the project root:

IVY_API_KEY=your_api_key

The API base URL defaults to:

https://solve.ivy.homes

The API key should not be committed to the repository.

4. Run the development server
npm run dev

Open:

http://localhost:3000
5. Production build
npm run build
Demo Authentication

The assignment-provided demo accounts can be used to test the application.

Authentication is performed against the real Ivy Homes API rather than using mock users.

API Investigation

The API documentation provided with the assignment was treated as a hypothesis rather than the source of truth.

I first tested the documented endpoints and compared their behaviour with the actual API responses. I then investigated pagination, authentication, filters, units, record counts, relationships between datasets, and data-quality patterns.

Some important discrepancies discovered during the investigation were:

Authentication

The documented login response does not match the actual response shape.

The live API returns an access_token, refresh_token, and expires_in, and supports a refresh flow.

Pagination

The API uses offset-based pagination.

The documented page parameter is ignored by the live API.

The maximum accepted/retrievable page size is also lower than the documented maximum.

The collection response provides pagination metadata such as:

limit
offset
count
total
has_more

rather than the documented page-based metadata.

Record Counts

The total value reported by the API does not represent every record that can be retrieved through pagination.

Therefore, the application uses the actual retrievable dataset when calculating the assignment statistics.

Listings

The listings endpoint can return records where is_live is false, despite the documentation describing the endpoint as returning active listings.

The frontend therefore handles inactive records explicitly.

Listing Detail Endpoint

The documented singular listing path does not work as described.

The working endpoint uses:

/v1/listings/{id}
Saved Listings

The documented favourites endpoint does not match the live API.

Saved listings are available through:

/v1/saved

with the appropriate listing identifier.

Analytics

The documented analytics summary endpoint was not available at the documented path.

The insights dashboard therefore calculates the required statistics directly from the available API datasets.

Units and Prices

Some project and rental values required interpretation based on the actual API data rather than blindly following the documentation.

Project prices were converted from Lakh/Crore representations where required, and area values were handled according to the units actually returned by the API.

Assignment Analysis

The repository contains the API investigation and final assignment answers.

The investigation covered:

Total listing records
Unique properties
Active listings
Corrupt listing records
Total monthly rent
Average price per square foot for 2 BHK listings
Costliest project
Listings created in the last 7 days
Fake listings
Projects with incorrect listing counts

Detailed evidence and investigation notes are available in the analysis/ directory.

Data Quality Findings

The API investigation identified several classes of inconsistencies, including:

Incorrect or incomplete API documentation
Pagination discrepancies
Missing documented endpoints
Undocumented working endpoints
Incorrect unit descriptions
Inconsistent record counts
Inactive records appearing in listing results
Duplicate or inconsistent property data
Invalid/corrupt listing records
Fake listings
Project listing-count inconsistencies

The findings were reproduced against the live API and documented with supporting evidence rather than being based on assumptions.

Deployment

The application is deployed using Vercel.

The API key is configured as a server-side environment variable in the deployment environment and is not stored in the source repository.

Security
API credentials are stored in environment variables.
.env and .env.local files are excluded through .gitignore.
The API key is not exposed as a hard-coded frontend value.
Authentication and API communication are handled through the application's server-side routes where appropriate.
AI Usage

LLM tools were used during development for:

Initial implementation assistance
Debugging
API investigation
Exploring API/documentation inconsistencies
Code review and refinement
Documentation

All generated suggestions were reviewed and validated against the actual application and live API behaviour.

What I Would Improve With More Time

With additional development time, I would:

Add automated tests for the API client and filtering logic
Add more comprehensive loading and error states
Improve accessibility across all interactive components
Add richer visualisations to the insights dashboard
Improve search and sorting capabilities
Add more detailed property comparison functionality
Add automated API consistency checks so documentation/API mismatches can be detected more easily
Improve caching and request deduplication for large datasets
Repository

GitHub repository:

https://github.com/anchi204/ivy-homes-internship

Built for the Ivy Homes Software Engineering Internship Assignment — September 2026.


**Bas `README.md` ka pura old content delete → ye pura paste → Save.**

Phir terminal:

```bash
git add README.md
git commit -m "Improve project documentation"
git push
