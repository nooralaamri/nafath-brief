Version: NAFATH-V2

Track: Mobile

## Overview

The 5G service for emergency responders depends on several technical areas working together, not just a strong signal. Software must handle requests safely when connections fail and clients retry. AI can help predict congestion, but its predictions need proper validation before being trusted. The mobile app must remain useful offline and synchronize records when connectivity returns. Network slicing can prioritize resources for emergency traffic, while cybersecurity processes help detect, contain, and recover from attacks. Finally, data models support clear daily reports showing usage across regions. These areas are connected: a reliable network is not enough if the app loses updates, predictions are inaccurate, or an attack compromises the service. The goal is to keep responders informed and operational under pressure, even when parts of the system are stressed or unavailable.

## Software

A safe HTTP method retrieves information without requesting a change to the server, as with GET. An idempotent method produces the same intended server-side effect when an identical request is repeated, as with PUT. These properties matter when a responder’s app retries after a connection failure. Repeating a non-idempotent POST could create duplicate incident reports, so the system should use suitable retry protection.

Resource: HTTP request methods - MDN Web Docs - https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods

## AI
A congestion-prediction model can overfit when it learns patterns specific to its training data but performs poorly on new network conditions. Cross-validation helps assess whether its predictions generalize by training and evaluating the model across different data splits. For a 5G emergency service, this evaluation matters because planners need predictions that remain useful during unfamiliar traffic peaks, not just periods similar to past observations.

Resource: 3.1. Cross-validation: evaluating estimator performance - scikit-learn - https://scikit-learn.org/1.1/modules/cross_validation.html

## Mobile

A responder’s app should save critical updates to persistent local storage when the network is unavailable. It should clearly show that a record is saved on the device but has not yet reached the server. When connectivity returns, the app can queue and retry pending writes, while tracking which updates have been synchronized. If another device changes the same record, the system needs a conflict-resolution rule rather than blindly overwriting data. For emergency records, preserving important updates and showing their synchronization status are essential.

Resource: Build an offline-first app - Android Developers - https://developer.android.com/topic/architecture/data-layer/offline-first

## Networking

5G network slicing allows an operator to create logical network slices with different service requirements over shared infrastructure. A dedicated slice for emergency responders can be configured to support their communication needs during periods of heavy public traffic. However, a slice does not automatically guarantee uninterrupted service; the operator must configure suitable resources, monitor performance, and manage failures so emergency communications remain dependable.

Resource: Network Resource Model (NRM) for 5G networks and network slicing - 3GPP - https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3399

## Cybersecurity

Incident response follows a lifecycle that helps an organization manage cyberattacks systematically. Preparation establishes roles and procedures; detection and analysis identify the incident and assess its impact. Containment limits further damage, eradication removes the threat, and recovery restores affected systems safely. Afterward, the team reviews what happened and improves its procedures. For a 5G emergency service, this process helps restore dependable communications while reducing the risk of repeated attacks.

Resource: Computer Security Incident Handling Guide - NIST - https://csrc.nist.gov/pubs/sp/800/61/r2/final

## Data

A star schema connects a central fact table, such as daily network usage, directly to dimension tables for date, region, and service type. A snowflake schema further divides some dimensions into related tables, reducing duplicated descriptive data but adding joins. For daily regional usage reports, a star schema is usually the more practical choice because its simpler structure makes filtering, aggregation, and reporting easier to manage.

Resource: Understand star schema and the importance for Power BI - Microsoft Learn - https://learn.microsoft.com/en-us/power-bi/guidance/star-schema

## Misconception in My Track

## Open Question
