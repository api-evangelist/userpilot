# Userpilot GraphQL Schema

## Overview

This GraphQL schema provides a conceptual representation of the Userpilot product growth platform. Userpilot enables teams to build in-app onboarding experiences, product tours, checklists, surveys, and feature analytics — without writing code. The schema covers the full breadth of Userpilot's domain: experiences (flows, modals, tooltips, banners), user and company identification, event tracking, segmentation, NPS and survey data, goals, and administrative resources.

The schema is derived from Userpilot's REST APIs (Realtime API at analytex.userpilot.io and Analytics Export API at appex.userpilot.io) and public documentation at https://docs.userpilot.com/api-references/overview.

## Schema Source

- **Type**: Conceptual / Community-contributed
- **Base REST APIs**:
  - Realtime API: `https://analytex.userpilot.io/v1`
  - Analytics Export API: `https://appex.userpilot.io/api/v1`
- **Documentation**: https://docs.userpilot.com/api-references/overview
- **Schema File**: `userpilot-schema.graphql`

## Type Summary

| Category | Types |
|---|---|
| Experiences | Experience, ExperienceDetails, ExperienceType, ExperienceStatus, ExperienceTrigger |
| Flows | FlowStep, FlowStepType, FlowConversion, ProductTour, TourStep, TourAnimation |
| UI Elements | Modal, Tooltip, HotSpot, Banner, Announcement |
| Checklists | Checklist, ChecklistItem, ChecklistProgress, ChecklistItemComplete |
| Surveys | Survey, SurveyQuestion, SurveyResponse, ContentSurvey, InAppSurvey, Microsurvey |
| NPS | NPSQuestion, NPSScore, NPS |
| Feature Tags & Heatmaps | FeatureTag, FeatureTagDetails, HeatMap |
| Event Tracking | EventTracking, CustomEvent, CustomEventDetails, AutoEvent, ClickEvent, PageEvent |
| Segmentation | Segment, SegmentCondition |
| Users | User, UserProfile, UserAttributes, UserCompany |
| Companies | Company, CompanyAttributes, CompanyDetails |
| Goals | Goal, GoalConversion |
| Resource Center | ResourceCenter, ResourceCenterItem |
| Administration | APIKey, Token, Webhook |

**Total named types: 55**

## Key Queries

- `experience(id: ID!)` — Fetch a single experience by ID
- `experiences(status: ExperienceStatus, type: ExperienceType)` — List experiences with optional filters
- `user(id: ID!)` — Fetch a user profile with attributes and company membership
- `users(segmentId: ID, limit: Int, offset: Int)` — List users, optionally scoped to a segment
- `company(id: ID!)` — Fetch a company record
- `segment(id: ID!)` — Fetch a segment definition
- `segments` — List all segments
- `survey(id: ID!)` — Fetch a survey and its questions
- `nps(from: String, to: String)` — Aggregate NPS data for a date range
- `checklist(id: ID!)` — Fetch a checklist and its items
- `goal(id: ID!)` — Fetch a goal and conversion metrics
- `resourceCenter(id: ID!)` — Fetch a resource center
- `webhook(id: ID!)` — Fetch a webhook configuration
- `apiKey` — Fetch the current API key metadata

## Key Mutations

- `identifyUser(input: UserProfileInput!)` — Create or update a user identity record
- `identifyCompany(input: CompanyInput!)` — Create or update a company record
- `trackEvent(input: CustomEventInput!)` — Send a custom event for a user
- `createExperience(input: ExperienceInput!)` — Create a new experience
- `updateExperience(id: ID!, input: ExperienceInput!)` — Update an existing experience
- `publishExperience(id: ID!)` — Publish a draft experience
- `pauseExperience(id: ID!)` — Pause a live experience
- `createWebhook(input: WebhookInput!)` — Register a new webhook endpoint
- `deleteWebhook(id: ID!)` — Remove a webhook
- `createSegment(input: SegmentInput!)` — Create a user segment
- `createGoal(input: GoalInput!)` — Define a new product goal

## Usage Notes

- Authentication uses API token keys passed as `Authorization: Token <api_key>` headers.
- User identification should be called before tracking events to associate events with known users.
- The `ExperienceType` enum distinguishes flows, modals, banners, checklists, surveys, tooltips, hotspots, product tours, resource centers, and announcements.
- Segment conditions combine user attributes, company attributes, event history, and experience engagement using AND/OR logic.
- NPS scores are integers in the range 0–10; Userpilot classifies promoters (9–10), passives (7–8), and detractors (0–6).
