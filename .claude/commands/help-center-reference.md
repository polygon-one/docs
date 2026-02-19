# Polygon1 Help Center Reference

Use this reference when creating help center content, user guides, onboarding documentation, or FAQ pages for Polygon1. This covers every user-facing feature, workflow, navigation path, setting, and import/export capability in the platform.

---

## PLATFORM OVERVIEW

Polygon1 is an EUDR (EU Deforestation Regulation) compliance platform that helps companies manage their supply chain due diligence obligations under EU Regulation 2023/1115. The platform enables operators and traders to:

- Track compliance status of articles (products) and suppliers
- Collect geolocation data for production plots and run satellite-based deforestation analysis
- Manage legal compliance through questionnaires and evidence documents
- Create and submit Due Diligence Statements (DDS) to the EU TRACES system
- Onboard suppliers via self-service invite forms
- Manage orders and link them to DDS statements
- Visualize supply chains and production plot locations on interactive maps
- Communicate with suppliers through built-in messaging
- Import/export data via CSV and integrate with ERP systems via API

**Supported Languages:** English, German, French, Spanish

---

## NAVIGATION STRUCTURE

The application uses a left sidebar with four main sections plus additional header items.

### Section 1: Compliance

| Page | Route | Purpose |
|---|---|---|
| **Inbound Dashboard** | `/inbound` | Central hub for monitoring EUDR compliance of purchased goods — shows supplier and article compliance status, pending actions, and geographic/legal analysis results |
| **Outbound Dashboard** | `/outbound` | Manages EU-produced articles and outbound DDS, including primary producer information and BOM (Bill of Materials) linking |
| **Articles** | `/articles` | CRUD management for all articles (products), including EUDR relevance flags, HS codes, commodity groups, and supplier associations |
| **Suppliers** | `/suppliers` | CRUD management for suppliers, including invitations for EUDR data collection, compliance tracking, and contact details |

### Section 2: Supply Chain

| Page | Route | Purpose |
|---|---|---|
| **Map** | `/map` | Interactive Mapbox map showing production plot locations with filters by supplier, article, analysis status, and risk flags — supports drawing plots and uploading GeoJSON |
| **Documents** | `/documents` | Flat list view of all uploaded evidence documents with search, pagination, and verification status tracking |
| **Supply Chain** | `/supply-chain` | Orbital/network visualization of the supply chain showing supplier tiers, compliance status, and data completeness |

### Section 3: Due Diligence

| Page | Route | Purpose |
|---|---|---|
| **Inbound DDS** | `/dds/inbound` | Manages inbound Due Diligence Statements for purchased commodities — shows orders without DDS and allows DDS creation/assignment |
| **Outbound DDS** | `/dds/outbound` | Manages outbound DDS for sold/exported articles — domestic production declarations |
| **Orders** | `/orders` | Purchase and sale order management with DDS assignment workflow |

### Section 4: Contact Center

| Page | Route | Purpose |
|---|---|---|
| **Messages** | `/messages` | Bidirectional messaging with suppliers for collaboration and data requests |

### Header Navigation

| Item | Route | Purpose |
|---|---|---|
| **Notifications** | `/notifications` | Notification center with filtering by type, read/unread status, and mark-as-read actions |
| **Settings** | `/settings` | User profile, company settings, API keys, CSV import configuration, automations |

### Admin Section (Admin/Super Users Only)

| Page | Route | Purpose |
|---|---|---|
| **Companies** | `/admin` | Overview of all companies with user counts, article/supplier stats |
| **Users** | `/admin` | User management including activation/deactivation |
| **Non-Compliance** | `/admin` | Dashboard of non-compliant articles across companies |
| **Usage** | `/admin` | Platform usage analytics and metrics |
| **Recalculate** | `/admin` | Trigger compliance recalculation for specific suppliers, companies, or all |

---

## FEATURE: INBOUND COMPLIANCE DASHBOARD

The Inbound Dashboard is the primary view for monitoring EUDR compliance of purchased goods.

### Summary Statistics

The top of the dashboard shows key metrics:
- **EUDR relevant suppliers** — Count of suppliers providing EUDR-relevant articles
- **Hectares analyzed** — Total area of production plots analyzed via satellite
- **Articles compliant** — Number and percentage of EUDR-relevant articles that are fully compliant

### Compliance Breakdown

Each supplier-article combination is assessed on three dimensions:

**Geographic Compliance:**
- Total production plots associated with the article
- Number of plots analyzed via satellite imagery
- Number of plots found compliant (no deforestation detected)
- Whether deforestation or forest degradation was detected
- Risk mitigation status if risks were identified

**Legal Compliance:**
- Questionnaire completion status (complete/incomplete)
- Evidence document count vs. required documents
- Verification status of uploaded documents (verified, rejected, expired, pending)
- Categories with identified non-compliance issues

**Overall Status:**
- **Compliant** — Both geo and legal compliance satisfied
- **Non-Compliant** — One or more compliance dimensions failed
- **Unknown** — Insufficient data to determine compliance
- **Not EUDR Relevant** — Article not subject to EUDR

### Pending Actions Panel

Shows a quick overview of articles that need attention:
- Articles missing geographic analysis
- Articles missing legal analysis
- Articles missing compliance reports
- Count of suppliers not yet invited

**Quick Action:** "Invite All Suppliers" button to mass-send invitations to all suppliers with EUDR-relevant articles that haven't been invited yet.

### Suppliers & Articles Table

A detailed table with:
- Search by supplier or article name
- Filters by country, commodity group
- Status filters: All, Unknown, Missing Geo, Missing Legal, Compliant, Non-Compliant
- Expandable rows showing article-level detail
- Per-row actions: Request Info, Generate Report, View Compliance, Show Plots, Upload Evidence, Fill Questionnaire

**DDS Reference:** Each supplier row has an inline-editable DDS reference field for linking upstream DDS.

### Additional Inbound Features

**Link Input Articles (BOM):**
- For sale/production articles, link which purchase articles are used as inputs
- Creates traceability from raw materials to finished goods
- Accessible via "Link Input Articles" action on outbound articles

**EU Production Information:**
- For articles produced within the EU, declare production details
- Select country of production
- Draw production plots on map or upload GeoJSON
- Enter production quantity in kg

**Downstream Operators:**
- View which companies purchase this product from you
- Shows company name, country, and their DDS reference

**Batch Risk Mitigation:**
- Mitigate multiple risk flags across all plots for an article in one action
- Select which risk flags to address
- Upload evidence or link existing certifications
- Submit for review

---

## FEATURE: OUTBOUND DASHBOARD

Manages EU-produced articles and outbound documentation.

### Key Functions
- View all sale/production articles with compliance status
- Link purchase articles to sale articles for full traceability (BOM linking)
- Declare primary producer information for EU-produced goods
- Manage outbound DDS statements

### Primary Producer Flow
1. Select an article marked for EU production
2. Click "I Produce This" or "Primary Producer Info"
3. Select country of production
4. Draw production plot on interactive map or upload GeoJSON
5. Enter production quantity
6. Accept declaration
7. Submit — triggers satellite analysis and DDS creation

---

## FEATURE: ARTICLES MANAGEMENT

### Overview
Central management for all products/articles in the system.

### Article Fields
| Field | Description |
|---|---|
| **Name** | Article/product name |
| **Internal Article Number** | Your company's internal reference |
| **External Article Number** | Supplier's article reference |
| **HS Code** | Harmonized System code for customs classification |
| **EAN** | European Article Number (barcode) |
| **Description** | Free-text product description |
| **Article Type** | Purchase (bought from suppliers) or Sale (sold to customers) |
| **EUDR Relevant** | Toggle whether article falls under EUDR scope |
| **Commodity Group** | Cattle, Cocoa, Coffee, Oil Palm, Rubber, Soya, Wood, or Non-Relevant |
| **Supplier** | Associated supplier (for purchase articles) |

### Actions
- **Create Article** — Manual form or CSV import
- **Edit Article** — Modify any field
- **Delete Article** — Remove (with confirmation dialog)
- **Import Articles** — Bulk CSV upload with configurable column mappings
- **View Compliance** — See geo/legal compliance breakdown

### CSV Import for Articles
Map CSV columns to system fields:
- Name, Article Number, Description, External Article Number
- HS Code, EAN, Article Type
- Supplier Name, Supplier Email
- Commodity Group, Scientific Name (for wood species)

---

## FEATURE: SUPPLIERS MANAGEMENT

### Overview
Manage supplier relationships and track their EUDR compliance data submission.

### Supplier Fields
| Field | Description |
|---|---|
| **Name** | Company name |
| **Contact Name** | Primary contact person |
| **Email** | Contact email address |
| **Country** | Country of the supplier |
| **Address** | Street address |
| **External ID** | Your ERP reference for this supplier |

### Supplier Statuses
- **Data Incomplete** — Supplier has not provided all required EUDR data
- **Data Complete** — All geo and legal data has been submitted
- **DDS Submitted** — Supplier has a submitted DDS statement

### Actions
- **Create Supplier** — Manual form or CSV import
- **Edit Supplier** — Modify details
- **Delete Supplier** — Remove (with confirmation)
- **Request Information / Invite** — Send email invitation to complete EUDR questionnaire
- **Show Plots** — View supplier's production plots on map
- **Import Suppliers** — Bulk CSV upload

### Inviting Suppliers
1. Click "Invite" or "Request Information" on a supplier
2. Select which EUDR-relevant articles to include
3. Optionally customize the invitation message
4. Send — supplier receives an email with a unique link
5. Supplier completes the multi-step invite form (geo data + legal questionnaire)
6. System automatically analyzes submitted data and updates compliance status
7. You receive a notification when the supplier completes onboarding

**Mass Invite:** From the Inbound Dashboard, click "Invite All Suppliers" to send invitations to all uninvited suppliers with EUDR-relevant articles.

---

## FEATURE: SUPPLIER PORTAL (INVITE FORM)

When a supplier receives an invitation, they access a multi-step self-service form.

### Step 1: General Information
- Confirm or enter company name
- Select country of operation

### Step 2: Geolocation Data
For each EUDR-relevant article:
- Select the commodity being produced
- Enter the commodity producer name
- Select country(ies) of production
- Provide geolocation data by either:
  - **Drawing on map** — Use the interactive drawing tool to outline production plots
  - **Uploading GeoJSON** — Import pre-prepared geolocation files

### Step 3: Sub-Supplier Mapping
If the supplier sources raw materials from upstream suppliers:
- Map input articles (raw materials) to the finished goods they supply
- Provide upstream supplier contact details (company name, email)
- Optionally include a personal message for the upstream supplier invitation

### Step 4: Legal Compliance Questionnaire
A comprehensive questionnaire covering 8 legal compliance categories:

1. **Land Use Rights & Ownership** — Legal rights to use the land for production
2. **Environmental & Nature Protection Laws** — Compliance with environmental regulations
3. **Forestry Law & Wood Use** — Applicable for wood/timber products only
4. **Rights of Third Parties & Indigenous Communities** — Respect for community rights
5. **Labor & Human Rights** — Working conditions and labor law compliance
6. **Tax, Trade & Customs Regulations** — Fiscal compliance
7. **Anti-Corruption Measures & Document Authenticity** — Anti-bribery and document integrity
8. **Other Compliance Measures** — Additional regulatory requirements

**Special Paths:**

- **FLEGT License Shortcut:** For wood products from FLEGT VPA countries, uploading a valid FLEGT license satisfies legal compliance requirements automatically
- **Sustainability Certification:** Suppliers can upload certifications (FSC, PEFC, SFI, ISCC, Rainforest Alliance, RSPO, Fairtrade, RTRS, EU Organic) — the system analyzes which compliance categories the certification covers and pre-marks them
- **Previously Completed:** If a questionnaire was already submitted, the system shows prior responses for review and update

### Confirmation
- Review all submitted data
- Warning shown if any questions remain unanswered
- Submit to complete the onboarding process

---

## FEATURE: ORDERS MANAGEMENT

### Overview
Track purchase and sale orders and link them to DDS statements for regulatory compliance.

### Order Fields
| Field | Description |
|---|---|
| **Order Number** | Unique order reference |
| **Order Date** | Date of the order |
| **Order Type** | Purchase (inbound) or Sale (outbound) |
| **Supplier** | The supplier for this order |
| **Positions** | Line items with article, quantity (kg), and DDS reference |

### Actions
- **Create Order** — Manual form or CSV import
- **Edit Order** — Modify order details and positions
- **Delete Order** — Remove with confirmation
- **Import Orders** — Bulk CSV upload
- **Assign to DDS** — Link order to an existing or new DDS statement

### CSV Import for Orders
Map CSV columns to:
- Order Number, Order Date, Order Type
- Supplier Name/Email
- Article Name/Number, Quantity
- DDS Reference Number, DDS Verification Number

---

## FEATURE: DUE DILIGENCE STATEMENTS (DDS)

### Overview
DDS statements are the core regulatory instrument under EUDR. Each DDS declares that specific products meet deforestation-free and legal compliance requirements.

### DDS Types
| Type | Description |
|---|---|
| **Import** | For commodities imported into the EU |
| **Export** | For commodities exported from the EU |
| **Trade** | For commodities traded within the EU |
| **Domestic Production** | For commodities produced within the EU |

### DDS Statuses
| Status | Meaning |
|---|---|
| **Draft** | Statement created but not yet submitted |
| **Processing** | Submission to TRACES is in progress |
| **Submitted** | Successfully submitted to TRACES |
| **Validated** | Validated by the EU system with a verification number |
| **Failed** | Submission failed — check error details |
| **Rejected** | Rejected by the competent authority |
| **External** | DDS created outside Polygon1, referenced by number only |
| **Under Control** | Under review by competent authority |
| **Correction Requested** | Authority has requested corrections |
| **Deleted** | Statement was withdrawn/deleted |

### Creating a DDS (3-Step Wizard)

**Step 1: General Information**
- Select activity type: Import, Export, Trade, or Domestic Production
- Select operator type
- Indicate if geolocations are confidential

**Step 2: Supplier & Articles**
- Select the supplier
- Choose which articles to include
- Enter quantities per article

**Step 3: Confirmation**
- Review all information
- Declare compliance per EU Regulation 2023/1115
- Submit the DDS

### Inbound DDS Page
- Shows "Orders without DDS Reference" — purchase orders that need to be assigned to a DDS
- Table of all inbound DDS statements with search and status filtering
- Actions: View details, download PDF, submit to TRACES

### Outbound DDS Page
- Shows sale orders without DDS reference
- Table of all outbound DDS statements
- Manage domestic production DDS

### DDS Details View
- Full statement overview with all articles, quantities, and geolocation data
- Plot information with compliance results
- Associated orders
- Signature and declaration text
- PDF download
- Submit to TRACES button (if not yet submitted)

### Overflow DDS
When a DDS reaches its capacity limit (maximum articles/plots), the system automatically creates an overflow DDS to accommodate additional items.

---

## FEATURE: INTERACTIVE MAP

### Overview
The Map page provides a full-screen interactive Mapbox map showing all production plots with their analysis results.

### Map Controls
- **Draw Polygon** — Use the drawing tool to create new plot boundaries directly on the map
- **Upload GeoJSON** — Import geolocation data from GeoJSON files
- **Zoom/Pan** — Standard map navigation controls

### Filters
- **By Supplier** — Show plots from specific suppliers
- **By Article** — Show plots for specific articles
- **By Analysis Status** — Filter by plot compliance status
- **By Risk Flags** — Show only plots with specific risk types

### Plot Details Sidebar
Clicking a plot opens a sidebar showing:
- Plot name and area (hectares)
- GPS coordinates (latitude/longitude)
- Associated articles and suppliers
- Analysis status and results
- Risk flags (if any)
- Satellite imagery analysis details

### Plot Statuses
| Status | Meaning |
|---|---|
| **No Deforestation Risk** | Satellite analysis confirmed no deforestation after cutoff date |
| **Deforestation Risk** | Analysis detected potential deforestation or degradation |
| **Pending Analysis** | Plot submitted, awaiting satellite analysis |
| **Not EUDR Relevant** | Plot associated with non-EUDR-relevant articles |
| **Pending Review** | Risk mitigation submitted, awaiting manual review |
| **Risk Mitigated** | Risk was identified but successfully mitigated with evidence |

### Satellite Analysis Datasets
Plots are analyzed using multiple satellite datasets:
- **ESA Land Cover** — European Space Agency land classification (Crop, Urban, Water, Tree Cover, Shrubland, Grassland)
- **JRC Forest Coverage** — Joint Research Centre forest type classification (Primary Forest, Natural Forest, Planted Forest)
- **PALSAR Radar** — JAXA radar imagery for forest change detection (Low/Moderate/High Risk)
- **TMF (Tropical Moist Forest)** — Tropical forest monitoring (Undisturbed, Degraded, Plantation, Regrowth, Deforested)

Additional checks:
- **Agroforestry Detection** — Identifies mixed agricultural-forest land use patterns
- **Sanity Checks** — Detects urban area overlap, water body overlap, and other anomalies

---

## FEATURE: SUPPLY CHAIN VISUALIZATION

### Overview
An interactive orbital/network graph showing the full supply chain structure.

### Views
- **Network View** — Circular/orbital layout showing suppliers at different tiers
- **Globe View** — Geographic visualization of supplier locations

### Node Information
Each supplier node shows:
- Company name and country
- Supply chain tier level
- Compliance status (Compliant, Non-Compliant, Unknown, Missing Data)
- Data completeness indicators (Geo Location, Legal Docs: Available/Missing)
- Commodities supplied

### Filters
- By tier level
- By compliance status
- Warnings only (show only problematic nodes)
- Supplier search

---

## FEATURE: EVIDENCE DOCUMENTS

### Overview
A centralized document management system for compliance evidence.

### Uploading Evidence
1. Click "Upload Document" (from Documents page or from article compliance view)
2. Select file (max 50 MB; supports PDF, PNG, JPEG, TIFF, CSV, GeoJSON, text files)
3. Optionally select a certification scheme (FSC, PEFC, ISCC, etc.)
4. Add user notes for context
5. Select which articles the evidence applies to
6. Upload — system runs AI analysis to classify and verify the document

### Document Verification Statuses
| Status | Meaning |
|---|---|
| **Verified** | Document confirmed as valid evidence |
| **Auto-Verified** | AI analysis confirmed the document automatically |
| **Pending Review** | Document needs manual human review |
| **Rejected** | Document was rejected as insufficient evidence |
| **Expired** | Document's validity period has passed |
| **Invalid** | Document could not be processed or is not relevant |

### AI Document Analysis
The system automatically:
- Classifies the document type
- Maps it to relevant legal compliance categories
- Assigns confidence scores
- Identifies critical issues, warnings, and validations
- Generates accept/reject recommendations

Documents are retained for a minimum of 5 years per EUDR requirements.

---

## FEATURE: MESSAGING

### Overview
Built-in communication channel with suppliers for data requests and collaboration.

### Features
- Compose messages with subject and body text
- Select supplier from dropdown
- Attachment support
- Message threading and history
- Bidirectional communication (supplier can reply)
- Messages linked to specific suppliers in the system

---

## FEATURE: NOTIFICATIONS

### Notification Bell
A notification icon in the top header shows the count of unread notifications. Click to view recent notifications with quick actions.

### Notifications Center Page
- **Tabs:** All, Unread
- **Filter by type** — Select specific notification categories
- **Pagination** — 20 notifications per page
- **Actions:** Mark as read, Mark all as read, Delete

### Notification Types

| Type | Trigger |
|---|---|
| **Article Non-Compliant** | An article fails compliance assessment |
| **Supplier Onboarded** | A supplier completes the onboarding invite form |
| **Invite Not Opened** | A supplier hasn't opened their invitation after 7 days |
| **Compliance Assessment Completed** | Geo or legal compliance assessment finishes processing |
| **DDS Submission Failed** | A DDS submission to TRACES fails |
| **DDS Submission Validated** | A DDS is successfully validated with verification number |
| **Risk Resolution Needs Review** | A risk resolution requires manual review |
| **Evidence Needs Review** | An evidence document couldn't be auto-verified |
| **DDS Capacity Full** | A DDS has reached its capacity limit |
| **Evidence Document Rejected** | An evidence document was rejected during review |

### Notification Channels
- **In-App** — Appears in the notification bell; stays until marked as read
- **Email** — Sent to the user's registered email address

Users can configure which events trigger notifications and through which channels in Settings > Notifications.

---

## FEATURE: SETTINGS

Settings are accessible from the header navigation and contain 5 tabs.

### Tab 1: Profile

**Contact Details:**
- Name, Email (personal)
- Company Name, Street, Postal Code, City, Country

**TRACES Integration:**
Configure credentials for automated DDS submission to the EU TRACES system:
- **EORI Number** — Economic Operators Registration and Identification number
- **TRACES Username** — Login for the EU TRACES system
- **TRACES Web Service Access Token** — API token obtained from the official EU system (one-time setup)

**Company Branding:**
- Upload company logo (PNG or JPEG, max 2 MB)
- Logo appears on outgoing emails such as supplier invitations and messages

### Tab 2: Notifications

Configure notification preferences:
- Toggle in-app and email notifications per event type
- Event types listed with descriptions
- Important events (e.g., compliance failures) vs. optional events
- Reset to defaults option

### Tab 3: API Keys

Manage API access tokens for ERP system integration:
- **Create Key** — Generate a new API key with a name and selected permissions
- **Scopes:** Articles (Read/Write), Suppliers (Read/Write), Orders (Read/Write), DDS Statements (Read/Write)
- **Key Display:** Token shown once on creation — must be copied immediately
- **Revoke Key** — Permanently disable an API key
- **Metadata:** Key prefix, creation date, last used timestamp

### Tab 4: CSV Imports

Configure column mappings for CSV imports. Separate configuration for each entity type:

**Articles CSV Mapping:**
- Name, Article Number, Description, External Article Number
- HS Code, EAN, Article Type, Supplier Name, Supplier Email
- Commodity Group, Scientific Name

**Suppliers CSV Mapping:**
- Name, Email, Contact Name, Country, Address, External ID

**Orders CSV Mapping:**
- Order Number, Order Date, Order Type, Supplier Name/Email
- Article Name/Number, Quantity, DDS Reference, DDS Verification Number

**Plots CSV Mapping:**
- Name, Geometry (WKT format), Commodity Group
- Production Start/End Date, Scientific Name, Country

Each mapping can be saved and reset to defaults.

### Tab 5: Automations

Configure automatic workflows:
- **Auto-Assign Orders to DDS** — When enabled, new orders are automatically assigned to matching open DDS statements based on supplier and article
- **Auto-Create DDS for Orders** — When enabled, if no matching DDS exists, one is automatically created for EUDR-relevant orders
- **Default DDS Volume (kg)** — Default volume for automatically created DDS statements

---

## DATA IMPORT CAPABILITIES

### CSV Import (Available for Articles, Suppliers, Orders, Plots)

**Workflow:**
1. Navigate to the relevant page (e.g., Articles)
2. Click the "Import" button
3. Select a CSV file from your computer
4. System maps columns using your saved CSV configuration (from Settings)
5. Validation runs — errors shown per row with details
6. Confirm import — valid rows are created, invalid rows are skipped
7. Success toast shows count of imported items

**Tips:**
- Configure column mappings in Settings > CSV Imports before first import
- CSV must use comma or semicolon delimiters
- First row should contain column headers
- Date fields should use ISO format (YYYY-MM-DD)
- WKT geometry for plots: `POLYGON((lng lat, lng lat, ...))` or `MULTIPOLYGON(...)`

### GeoJSON Import (Map / Invite Form)

Upload `.geojson` files containing production plot boundaries:
- Supports Feature and FeatureCollection types
- Polygon and MultiPolygon geometries
- Properties from features are mapped to plot metadata

### XLSX Import (Orders)

Excel file import available for orders with DDS data export in structured sheets:
- Orders sheet: Order numbers, suppliers, articles, quantities
- DDS Statements sheet: Reference numbers, verification numbers, statuses

---

## DATA EXPORT CAPABILITIES

### Report Generation
- Generate compliance reports for individual articles or suppliers
- PDF format with geo/legal compliance details
- Accessible from dashboard action menus

### DDS PDF Export
- Download any DDS statement as a PDF document
- Includes all declaration details, articles, quantities, and compliance information

### TRACES Export
- Submit DDS directly to the EU TRACES system from within Polygon1
- Requires TRACES credentials configured in Settings > Profile

### Data Export (Orders & DDS)
- Export orders and DDS data as structured XLSX files
- Columns include: Order Number, Supplier, Products, HS Code, Quantities, DDS References, Verification Numbers, Statuses

---

## KEY WORKFLOWS

### Workflow 1: Initial Setup
1. Register an account and log in
2. Go to **Settings > Profile** — enter company details and TRACES credentials
3. Go to **Settings > CSV Imports** — configure column mappings for your data format
4. Go to **Settings > Automations** — enable auto-assign and auto-create DDS if desired
5. Import articles via **Articles > Import**
6. Import suppliers via **Suppliers > Import**
7. Import orders via **Orders > Import** (optional)

### Workflow 2: Supplier Onboarding
1. Go to **Suppliers** — verify supplier list is complete
2. Go to **Inbound Dashboard** — review pending actions
3. Click **"Invite All Suppliers"** or invite individually via "Request Information"
4. Suppliers receive email invitations with unique links
5. Each supplier completes the self-service form (geo data + legal questionnaire)
6. System automatically runs satellite analysis on submitted plot data
7. Compliance status updates appear on the Inbound Dashboard
8. You receive notifications as suppliers complete onboarding

### Workflow 3: Compliance Review
1. Go to **Inbound Dashboard** — review compliance status per supplier/article
2. For articles with **Missing Geo** — check if supplier invitation is pending or request additional data
3. For articles with **Missing Legal** — verify questionnaire completion status
4. For **Non-Compliant** articles — review specific issues:
   - Geographic: Check which plots have deforestation risk, initiate risk mitigation
   - Legal: Review failed categories, request additional documents from supplier
5. Use **Batch Risk Mitigation** to address multiple risk flags at once
6. Upload or request additional evidence documents as needed

### Workflow 4: Risk Mitigation
1. Identify articles with geographic risk flags (deforestation/degradation detected)
2. Click "Mitigate" on the specific risk flag or use "Batch Risk Mitigation"
3. Choose mitigation approach:
   - Upload evidence document proving compliance
   - Request evidence from supplier
   - Link existing certification
4. Submit mitigation for review
5. System evaluates the evidence (AI analysis + manual review if needed)
6. Status updates to "Risk Mitigated" if evidence is accepted, or stays "Non-Compliant" if rejected

### Workflow 5: DDS Creation and Submission
1. Go to **Inbound DDS** (or Outbound DDS for exports)
2. Review "Orders without DDS Reference" section
3. Click "Create DDS" to start the 3-step wizard:
   - Step 1: Select activity type (Import/Export/Trade/Domestic Production)
   - Step 2: Select supplier, articles, and enter quantities
   - Step 3: Review and confirm the declaration
4. DDS is created in Draft status
5. Verify all linked articles are compliant
6. Click "Submit to TRACES" to send the DDS to the EU system
7. Monitor status: Processing → Submitted → Validated (with verification number)
8. Download PDF for records if needed

### Workflow 6: Domestic EU Production
1. Go to **Outbound Dashboard**
2. Find your production article
3. Click **"Primary Producer Info"** or **"I Produce This"**
4. Select country of production
5. Draw production plots on the map or upload GeoJSON
6. Enter production quantity in kg
7. Accept and submit the declaration
8. System runs satellite analysis on the declared plots
9. A DDS is created automatically

### Workflow 7: Order Management with DDS Linking
1. Go to **Orders** — create or import purchase/sale orders
2. Each order contains positions (article + quantity in kg)
3. If automations are enabled, orders auto-link to matching DDS statements
4. If not, go to **Inbound DDS** → "Orders without DDS Reference"
5. Select order and assign to an existing DDS or create a new one
6. Order volumes are tracked against DDS capacity

### Workflow 8: Supply Chain Monitoring
1. Go to **Supply Chain** for an overview of the entire supplier network
2. Use filters to find problematic nodes (non-compliant, missing data)
3. Click on supplier nodes for detail cards showing compliance status
4. Go to **Map** to see geographic distribution of production plots
5. Filter by risk flags to identify areas of concern
6. Drill into individual plots for satellite analysis details

---

## COMMODITY GROUPS

EUDR applies to seven commodity groups. Each article in Polygon1 is assigned to one:

| Commodity | Examples |
|---|---|
| **Cattle** | Live cattle, beef, leather, hides |
| **Cocoa** | Cocoa beans, powder, butter, chocolate |
| **Coffee** | Roasted/unroasted coffee, coffee products |
| **Oil Palm** | Palm oil, palm kernel oil, palm-derived products |
| **Rubber** | Natural rubber, tires, rubber products |
| **Soya** | Soybeans, soy oil, soy meal |
| **Wood** | Timber, plywood, paper, pulp, wooden furniture |
| **Non-Relevant** | Products not subject to EUDR |

---

## COMPLIANCE ASSESSMENT MODEL

### Geographic Compliance
- Based on satellite imagery analysis of production plots
- Checks for deforestation and forest degradation after the cutoff date (December 31, 2020)
- Uses multiple satellite datasets (ESA, JRC, TMF, PALSAR)
- Plots must show no deforestation to be compliant
- If risks are detected, they can be mitigated with evidence

### Legal Compliance
- Based on the legal questionnaire and evidence documents
- Covers 8 legal categories per production country's legislation
- Documents are analyzed by AI for relevance and validity
- Certifications (FSC, PEFC, etc.) can pre-satisfy multiple categories
- FLEGT licenses provide a fast-track path for wood from VPA countries

### Supply Chain Complexity
- **Low** — Direct sourcing (single tier)
- **Medium** — Few intermediaries (2-3 tiers)
- **High** — Multiple intermediaries (4+ tiers)
- Higher complexity requires more thorough due diligence

### Overall Compliance
An article is **Compliant** only when:
1. All production plots pass geographic analysis (or risks are mitigated)
2. All legal compliance categories are satisfied (questionnaire + documents)
3. The full supply chain has been assessed

---

## COUNTRY RISK CLASSIFICATION

Under EUDR, countries are classified into three risk tiers that affect due diligence requirements:

| Risk Level | Due Diligence Required | EU Check Rate | Notable Countries |
|---|---|---|---|
| **Low Risk** | Simplified (no risk assessment/mitigation needed) | 1% of operators | All EU member states, 140+ countries |
| **Standard Risk** | Full due diligence | 3% of operators | Brazil, Indonesia, Malaysia, ~50 countries |
| **High Risk** | Full due diligence + enhanced scrutiny | 9% of operators | Belarus, North Korea, Myanmar, Russia |

---

## EUDR REGULATORY CONTEXT

**What is EUDR?** EU Regulation 2023/1115 (as amended by 2025/2650) requires companies placing certain commodities on the EU market to prove they are deforestation-free and legally produced.

**Key Requirements:**
- Products must be deforestation-free (no deforestation after Dec 31, 2020)
- Products must comply with relevant legislation of the country of production
- A Due Diligence Statement (DDS) must be submitted to the EU TRACES system before placing products on the market
- Geolocation data for all production plots (latitude/longitude to 6 decimal places; polygon for plots >4 hectares)
- Records must be retained for at least 5 years

**Application Dates:**
- Large/medium enterprises: December 30, 2026
- Micro/small enterprises: June 30, 2027

---

## GLOSSARY

| Term | Definition |
|---|---|
| **Article** | A product or goods item tracked in the system |
| **BOM** | Bill of Materials — linking input articles to output articles |
| **Commodity Group** | One of the 7 EUDR commodity categories (cattle, cocoa, coffee, oil palm, rubber, soya, wood) |
| **Competent Authority** | National authority responsible for EUDR enforcement |
| **DDS** | Due Diligence Statement — regulatory declaration submitted to TRACES |
| **Downstream Operator** | A company further down the supply chain that receives products |
| **EORI** | Economic Operators Registration and Identification number |
| **EUDR** | EU Deforestation Regulation (EU 2023/1115) |
| **FLEGT** | Forest Law Enforcement, Governance and Trade — EU scheme for legal timber |
| **GeoJSON** | Open standard format for geographic data structures |
| **HS Code** | Harmonized System code used for international trade classification |
| **Operator** | A company that places EUDR-relevant products on the EU market |
| **Plot** | A geographic production area with defined boundaries |
| **Risk Mitigation** | Process of providing evidence to address identified deforestation risks |
| **TRACES** | Trade Control and Expert System — EU platform for DDS submission |
| **Trader** | A company that makes EUDR-relevant products available on the EU market without placing them |
| **VPA** | Voluntary Partnership Agreement — bilateral agreement between EU and timber-producing countries |
| **WKT** | Well-Known Text — format for representing geometric shapes as text |

---

## KEYBOARD SHORTCUTS & UI TIPS

- **Search:** Most tables have a search bar at the top for filtering by name
- **Filters:** Use the filter dropdowns above tables to narrow results by country, commodity, or status
- **Expandable Rows:** Click on supplier rows in the dashboard to see article-level details
- **Inline Edit:** DDS reference fields can be edited directly in the table without opening a dialog
- **Notifications Bell:** Click the bell icon in the header for quick access to recent notifications
- **Language Switcher:** Change the interface language from the user menu (EN, DE, FR, ES)

---

## TROUBLESHOOTING / FAQ

**Q: My supplier hasn't received the invitation email.**
A: Check the supplier's email address is correct in the Suppliers page. The invitation may be in their spam folder. You can resend the invitation from the supplier's action menu.

**Q: A plot shows "Pending Analysis" for a long time.**
A: Satellite analysis may take a few minutes. If it persists, check the Notifications page for any error notifications. You can also trigger a re-analysis from the plot details.

**Q: My DDS submission to TRACES failed.**
A: Verify your TRACES credentials in Settings > Profile. Check that EORI number, username, and access token are correct. Review the error message in the DDS details for specific issues.

**Q: How do I handle articles with multiple suppliers?**
A: Each supplier-article combination is tracked separately. The same article can be purchased from different suppliers, and each combination has its own compliance assessment.

**Q: What file formats are supported for evidence uploads?**
A: PDF, PNG, JPEG, TIFF, CSV, GeoJSON, and text files. Maximum file size is 50 MB.

**Q: How do I configure CSV imports for my data format?**
A: Go to Settings > CSV Imports. Select the entity type (Articles, Suppliers, Orders, or Plots) and map your CSV column names to the corresponding system fields. Save your configuration for future imports.

**Q: Can I undo a DDS submission?**
A: Once submitted to TRACES, a DDS cannot be simply undone. You would need to request a correction or create a new DDS. Draft DDS statements can be deleted before submission.

**Q: What certifications are recognized for legal compliance?**
A: The system recognizes FSC, PEFC, SFI, ISCC, Rainforest Alliance, RSPO, Fairtrade, RTRS, and EU Organic certifications. Each certification is analyzed to determine which legal compliance categories it covers.

**Q: How does the BOM linking work?**
A: BOM (Bill of Materials) linking connects purchase articles (inputs) to sale/production articles (outputs). Go to the Outbound Dashboard, find your output article, and click "Link Input Articles" to select which purchase articles are used in its production.

---

## SOURCES

- EU Deforestation Regulation: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02023R1115-20251226
- Regulation 2025/2650 (Amendment): https://eur-lex.europa.eu/eli/reg/2025/2650/oj/eng
- EC EUDR Information System: https://green-forum.ec.europa.eu/deforestation-regulation-implementation/information-system-deforestation-regulation_en
- EC Country Benchmarking: https://green-forum.ec.europa.eu/nature-and-biodiversity/deforestation-regulation-implementation/eudr-cooperation-and-partnerships_en
