# OSINT & IMINT: Target Profiling & Geolocation (James Kensi)

## Mission Description
The objective of this investigation was to identify the last known location of a person of interest, starting with only a single artifact: the email address `james.kensi.92@gmail.com`. The mission required digital footprinting across social media platforms and the geolocation of an open-source photograph.

## Tools & Platforms
*   **OSINT:** Manual identity verification and pivoting on social media platforms (Twitter / X).
*   **IMINT (Imagery Intelligence):** Yandex Reverse Image Search.
*   **OPSEC Analysis:** Pattern recognition within username structures.

## Methodology

### 1. Username Analysis & OPSEC Failures
Starting with the provided email address (`james.kensi.92@gmail.com`), I analyzed the local part of the address. I identified a significant personal operational security (OPSEC) flaw: the inclusion of a birth year (`92` -> 1992). 

Furthermore, leveraging the fact that Gmail ignores periods in email addresses, I deduced that the primary username the target likely uses across the web is `jameskensi92`. This analysis drastically narrowed the search scope for cross-platform identity correlation.

### 2. Social Media Pivoting (Twitter / X)
Since automated email OSINT tools often encounter execution restrictions or paywalls, I pivoted to manual username searches across social media platforms using the deduced handle. I successfully identified an active Twitter (X) account belonging to the target (`@jameskensi92`), which featured a photograph from 2023 depicting a bridge.

### 3. Geolocation via Reverse Image Search (IMINT)
To determine the precise location captured in the photograph:
1. I extracted the bridge image from the Twitter account.
2. I uploaded the image to the Yandex visual search engine (highly effective for geographical and architectural recognition).
3. By cross-referencing the structural layout of the bridge and the similar results provided by the algorithm, I confirmed that the photograph was taken in San Francisco, California.

## Remediation & Privacy Recommendations (OPSEC)
To prevent unauthorized tracking and geolocation (doxxing), individuals should:
1.  **Avoid Personal Identifiers:** Do not include birth years, zip codes, or other identity markers in public handles.
2.  **Image Scrubbing:** Avoid posting photographs containing unique geographical landmarks (e.g., recognizable bridges, distinctive buildings) if physical location privacy is a priority.

## Conclusion & Flag
*   **Target Email:** `james.kensi.92@gmail.com`
*   **Platform Identified:** Twitter (X)
*   **Final Location:** San Francisco, USA
