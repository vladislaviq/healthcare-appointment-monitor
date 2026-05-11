# Healthcare Appointment Monitor (n8n Microservices)

This repository contains the JSON workflows for an automated monitoring system built with n8n. 

## Business Problem
Patients in Lithuania often miss free medical appointments because the national health portal requires constant manual refreshing, and slots are booked within minutes.

## Solution Architecture
I built a two-part microservice architecture to automate the search and notification process:

1. **Frontend (eSveikata_TG_Bot.json):** An interactive Telegram bot that allows users to select a specific medical service. It registers the user and saves their target service ID and Chat ID to a Google Sheet database.
   
2. **Backend (eSveikata_Monitoring.json):** A cron-triggered worker (runs every 15 minutes) that:
   - Polls the closed healthcare REST API (bypassing restrictions using custom browser headers).
   - Uses **Custom JavaScript** to filter only state-funded ("Ligonių kasos") slots that require a referral.
   - Cross-references new slot IDs with historical data in Google Sheets to prevent duplicate alerts.
   - Sends instant push notifications via Telegram when a new slot is found.

## Tech Stack
n8n, REST API, JavaScript, Telegram Bot API, Google Workspace (Sheets as a State DB).
