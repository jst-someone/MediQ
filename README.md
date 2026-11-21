# MediQ – Smart Hospital Discovery & Real-Time OPD Queue Management System

A digital healthcare platform combining a native Android mobile application, a cloud-backed database with Row Level Security, and an administrative portal to modernize patient hospital discovery and streamline Outpatient Department (OPD) queue management.

## Project Overview

MediQ eliminates physical waiting lines at hospitals and simplifies access to healthcare services. Patients can discover nearby healthcare facilities, view real-time department queue lengths, book doctor consultations, and track queue movement live on their mobile devices. Healthcare providers and administrative staff benefit from dedicated workflows to manage appointments, update patient statuses, and operate medical facilities efficiently.

## Key Features

- **Hospital Discovery & Mapping**:
  - Interactive map view integrating OpenStreetMap and Overpass API for real-time proximity searches.
  - Comprehensive hospital directory with specialties, contact details, operating hours, and facility information.
- **Live OPD Queue Tracking**:
  - Real-time token generation and virtual queue tracking.
  - Live wait-time estimation and queue position alerts, reducing in-person waiting room congestion.
- **Multi-Role Workflows**:
  - **Patient**: Search hospitals, filter by medical specialty, view doctor profiles, book appointments, receive status notifications, and write verified reviews.
  - **Doctor**: Dedicated portal to view daily appointment rosters, call the next patient in line, update consultation statuses, and manage schedule availability.
  - **Receptionist / Staff**: Onboarding interface to register walk-in patients, manage queue tokens, update desk allocations, and verify patient arrivals.
  - **Hospital Administrator**: Web-based administration panel to approve staff, manage department quotas, configure hospital listings, and monitor hospital-wide queue metrics.
- **Emergency SOS Module**: Quick-access directory of emergency departments and nearest hospital contacts for critical care situations.

## System Architecture

```
                      ┌──────────────────────────────────────┐
                      │            MediQ Client              │
                      │  (Android Application & Admin Web)   │
                      └──────────────────┬───────────────────┘
                                         │
                   ┌─────────────────────┴─────────────────────┐
                   ▼                                           ▼
      ┌─────────────────────────┐                 ┌─────────────────────────┐
      │  Overpass / OSM API     │                 │   Supabase Backend      │
      │  (Geospatial Discovery) │                 │   (PostgreSQL & Auth)   │
      └─────────────────────────┘                 └────────────┬────────────┘
                                                               │
                                       ┌───────────────────────┴───────────────────────┐
                                       ▼                                               ▼
                         ┌───────────────────────────┐                   ┌───────────────────────────┐
                         │   Row Level Security      │                   │   Realtime Queue Engine   │
                         │   (Role-Based Policies)   │                   │   (Appointments & Tokens) │
                         └───────────────────────────┘                   └───────────────────────────┘
```

## Technology Stack

- **Mobile Application**: Native Android (Java / Android SDK)
- **UI & Design**: Material Design Components, Custom Dialogs, Bottom Sheets
- **Geospatial & Mapping**: OpenStreetMap, Overpass API Client
- **Backend & Database**: Supabase (PostgreSQL with custom functions, triggers, and migrations)
- **Authentication & Security**: Supabase Auth with granular PostgreSQL Row-Level Security (RLS) policies
- **Web Administration Portal**: Responsive HTML5, CSS3, JavaScript, Supabase JS SDK

## Directory Structure

```
├── app/
│   ├── src/main/java/com/example/mediq/
│   │   ├── data/                 # Remote API clients, database models, and repository logic
│   │   ├── ui/                   # Activity & Fragment controllers
│   │   │   ├── appointments/     # Appointment scheduling and history views
│   │   │   ├── auth/             # Login, signup, splash, and onboarding
│   │   │   ├── common/           # Shared bottom sheets, dialogs, and components
│   │   │   ├── patient/          # Search, map view, hospital detail, and profile
│   │   │   ├── queue/            # Real-time queue tracker and token displays
│   │   │   └── staff/            # Doctor and Receptionist home dashboards
│   │   └── MediQApp.java         # Global application state entrypoint
│   └── src/main/res/             # Layouts, vector drawables, themes, and colors
├── admin/                        # Web-based hospital administrator portal
├── sql/                          # Supabase PostgreSQL schema, RLS policies, and migrations
├── build.gradle.kts              # Application build configuration
└── settings.gradle.kts           # Gradle project settings
```
