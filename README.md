# Bistro OS: restaurant ordering system

A table-ordering web app for a small restaurant, built from requirements to delivery. Customers build a ticket from the menu and send it to the kitchen; the kitchen moves each order through its status, and the customer sees the progress.

**Live demo:** enable GitHub Pages for this repo (Settings > Pages > Deploy from branch > `main` / root) and the app will be served from `index.html`.

> The restaurant, menu and prices are fictional. There are no real payments.

## Features
- Menu by section with prices, add/remove items, live subtotal, 5% tax and total
- Table number required to place an order; optional customer name
- Kitchen board (New, Preparing, Ready) with one-click status updates
- Customer-side status tracker (New, Preparing, Ready, Served)
- Orders survive page reloads (browser `localStorage`); open the Kitchen tab in a second browser tab and it stays in sync
- Single file, no dependencies, works on phone and desktop

## Run it
Open `index.html` in a browser. No build step.

## Documentation
The full requirements document, user stories with acceptance criteria, SDLC phases and test cases are in [`docs/BRD.md`](docs/BRD.md).

## Tech
HTML, CSS and vanilla JavaScript.

## Limitations and next steps
Orders live in one browser, so a real restaurant would need a small back end (API plus database) so many phones can reach one kitchen screen. Other next steps: payments, staff login and a sales dashboard.
