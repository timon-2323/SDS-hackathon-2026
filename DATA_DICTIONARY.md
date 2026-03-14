# 🚢 AIS Data Dictionary

This document provides the technical specifications for the AIS (Automatic Identification System) dataset. This version has been updated to match the exact column headers found in the 2024 Danish Waters snapshot.

## 1. Core Identification & Static Data
These fields identify the vessel and its physical configuration. Static data is usually programmed into the transponder.

| Field Name | Description | Example | Type |
| :--- | :--- | :--- | :--- |
| **MMSI** | Maritime Mobile Service Identity: A unique 9-digit ID for the ship. | `205246000` | str |
| **Name** | Name of the vessel as shown on the radio license. | `Z510 DENNIS` | str |
| **IMO** | International Maritime Organization vessel number (Permanent ID). | `9215969` | str |
| **Callsign** | Radio call sign assigned to the vessel. | `OPUF` | str |
| **Type of mobile**| Category of transponder (e.g., Class A, Class B, Base Station). | `Class A` | str |
| **Ship type** | Descriptive category of the vessel. | `Fishing` | str |

## 2. Dynamic Movement Data
Real-time GPS and navigation metrics updated automatically by onboard sensors.

| Field Name | Description | Units | Type |
| :--- | :--- | :--- | :--- |
| **# Timestamp** | Full UTC date and time of the broadcast point. | YYYY-MM-DD HH:MM:SS | datetime |
| **Latitude** | Latitude (decimal degrees). | Degrees | f64 |
| **Longitude** | Longitude (decimal degrees). | Degrees | f64 |
| **SOG** | Speed Over Ground: Current vessel speed. | Knots | f64 |
| **COG** | Course Over Ground: Actual path over the water. | Degrees | f64 |
| **Heading** | True Heading: The direction the ship's bow is pointing. | Degrees | f64 |
| **ROT** | Rate of Turn: The speed at which the ship is turning. | °/min | f64 |
| **Navigational status** | Current activity (e.g., Under way using engine, At anchor). | N/A | str |

## 3. Voyage & Dimensional Data
Physical attributes and antenna placement.

| Field Name | Description | Example | Units |
| :--- | :--- | :--- | :--- |
| **Cargo type** | Type of goods being transported. | `Undefined` | str |
| **Draft** | Depth of the vessel below the waterline. | `3.5` | Meters |
| **Length** | Total length of the vessel (calculated as $A + B$). | `38.0` | Meters |
| **Width** | Total width of the vessel (calculated as $C + D$). | `9.0` | Meters |

### The Antenna Dimensions (A, B, C, D)
These columns specify the exact location of the GPS antenna on the vessel. These are critical for high-precision navigation and identifying ship size.

* **A**: Distance from the Antenna to the **Bow** (Front).
* **B**: Distance from the Antenna to the **Stern** (Back).
* **C**: Distance from the Antenna to the **Port** (Left side).
* **D**: Distance from the Antenna to the **Starboard** (Right side).

---
*Source: MarineCadastre.gov / Danish Maritime Authority 2024 Snapshot*
