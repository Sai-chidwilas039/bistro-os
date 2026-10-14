# Business Requirements Document: Bistro OS

| | |
|---|---|
| **Project** | Bistro OS, a table-ordering system for a small restaurant |
| **Author** | Addepalli Sai Chidwilas |
| **Version / status** | 1.0 / Delivered (demo) |
| **Scenario** | Illustrative. The bistro, menu and prices are fictional. |

## 1. Business problem
A small bistro takes orders on paper. During peak hours, orders are mis-heard, tickets are lost between the floor and the kitchen, and customers wait without knowing the status of their food. The owner has no record of what sells.

## 2. Business objectives (targets)
| ID | Objective | Target |
|---|---|---|
| O1 | Reduce order-entry errors | Orders captured exactly as entered by the customer |
| O2 | Give the kitchen one live queue | No paper tickets; every order visible by status |
| O3 | Give customers visibility | Customer can see their order status at any time |
| O4 | Keep it usable without training | A first-time user places an order in under 2 minutes |

## 3. Scope
**In scope:** menu display, ticket (cart) with tax, order placement with table number, kitchen board with status flow, order status for the customer.
**Out of scope:** online payments, delivery, inventory, user accounts, multi-restaurant support.

## 4. Stakeholders
| Stakeholder | Interest |
|---|---|
| Customer | Quick, accurate ordering and status visibility |
| Kitchen staff | A clear, ordered queue of what to cook |
| Owner / manager | Fewer errors, a base for sales reporting |

## 5. Functional requirements (MoSCoW)
| ID | Requirement | Priority |
|---|---|---|
| FR-01 | Display the menu grouped by section with name, description and price | Must |
| FR-02 | Add items to a ticket and increase/decrease quantities | Must |
| FR-03 | Show subtotal, 5% tax and total, updated live | Must |
| FR-04 | Require a table number to place an order; name is optional | Must |
| FR-05 | Block order placement when the ticket is empty | Must |
| FR-06 | Assign each order a unique number and the status "New" | Must |
| FR-07 | Kitchen board with New, Preparing and Ready columns and a button to advance each order | Must |
| FR-08 | Customer sees order status progress (New, Preparing, Ready, Served) | Should |
| FR-09 | Orders persist across page reloads | Should |
| FR-10 | Kitchen can clear all orders (demo reset) | Could |

## 6. Non-functional requirements
- **Usability:** works on phone and desktop; buttons have text labels and keyboard focus is visible.
- **Performance:** all interactions respond instantly (no network calls).
- **Security:** user-entered text is escaped before display (prevents script injection).
- **Portability:** a single HTML file, no build step or server.

## 7. User stories and acceptance criteria
**US-01** As a customer, I want to add dishes to a ticket so that I can order without waiting for a waiter.
*Given* I am on the menu, *when* I press Add on a dish, *then* it appears on my ticket and the total updates.

**US-02** As a customer, I want to change quantities so that I can correct my order before sending it.
*Given* a dish is on my ticket, *when* I press "-" on a quantity of 1, *then* the dish is removed.

**US-03** As a customer, I want to see my order's progress so that I know when to expect my food.
*Given* I placed an order, *when* the kitchen changes its status, *then* my status bar updates.

**US-04** As kitchen staff, I want orders grouped by status so that I can see what to cook next.
*Given* a new order arrives, *when* I open the Kitchen tab, *then* it appears under New with its table number and items.

**US-05** As kitchen staff, I want to move an order forward so that the customer and the team see the same status.
*Given* an order under New, *when* I press "Start preparing", *then* it moves to Preparing.

## 8. SDLC approach
| Phase | Deliverable |
|---|---|
| Requirements | This BRD, user stories, MoSCoW priorities |
| Design | Two screens (Order, Kitchen), order status flow New > Preparing > Ready > Served |
| Build | `index.html` (HTML, CSS, JavaScript; browser storage for persistence) |
| Test | Test cases below |
| Deploy | Static hosting on GitHub Pages |

## 9. Test cases
| ID | Covers | Steps | Expected result | Result |
|---|---|---|---|---|
| TC-01 | FR-01, FR-02 | Add Butter chicken twice and Masala chai once | Ticket shows 2 and 1 with correct line totals | Pass |
| TC-02 | FR-02 | Press "-" on an item with quantity 1 | Item is removed from the ticket | Pass |
| TC-03 | FR-03 | Ticket with 2 x 380 and 1 x 60 | Subtotal 820, tax 41, total 861 | Pass |
| TC-04 | FR-05 | Open page with an empty ticket | Place order is disabled | Pass |
| TC-05 | FR-04, FR-06, FR-08 | Choose table 4, place order | Order #101 created; status shows New | Pass |
| TC-06 | FR-07, US-05 | In Kitchen, advance order #101 twice | Order moves New > Preparing > Ready; customer status updates | Pass |

## 10. Assumptions, constraints and risks
- **Assumption:** the kitchen and the customer's device use the same browser or share a session in the demo; a real deployment needs a shared back end.
- **Constraint:** orders are stored in the browser (`localStorage`), so they are per-device.
- **Risk:** without a back end, orders from different phones cannot reach one kitchen screen. *Mitigation:* the next phase adds a small API and database.

## 11. Future enhancements
Back-end API and database, payments, staff login, sales reporting dashboard (daily revenue, top dishes), printing kitchen tickets.
